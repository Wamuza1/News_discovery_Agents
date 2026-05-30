## News Discovery Agent


### NewsFindr: AI-Powered Personalized News Discovery Agent

NewsFindr addresses information overload by providing real-time, personalized news updates tailored to user interests. Leveraging **LangChain** and specifically **LangGraph's agentic flow**, it ensures accuracy and credibility in recommendations. This project aims to enhance user engagement and optimize content discovery by delivering secure, fair, and explainable news.

## **Business Problem**

NewsFindr is redefining news discovery by delivering real-time news updates tailored to user interests. Traditional search methods and generic news feeds often lead to information overload and inefficiencies, making it challenging for users to access relevant and trustworthy content efficiently.

To address this, NewsFindr leverages LangGraph agentic flow to build an AI-powered news retrieval agent that ensures accuracy and credibility. By utilizing this structured, multi-step approach, the system will provide secure, fair, and explainable recommendations—enhancing user engagement, optimizing content discovery, and improving access to timely and relevant news.

## **Business Impact**

✔ **Personalized News Experience** – Delivers real-time, relevant news tailored to user interests.

✔ **Time Efficiency** – Eliminates manual searches, ensuring instant access to the latest updates.

✔ **Trust & Transparency** – Ensures accuracy, credibility, and fairness in AI-driven news recommendations.

## **Objective**

🔹 **Provide real-time, personalized news retrieval** to help users discover relevant content effortlessly.

🔹 **Ensure accuracy and credibility** by sourcing news from trusted platforms and minimizing misinformation.

🔹 **Improve user engagement** through seamless content discovery, reducing information overload.

🔹 **Streamline the news consumption process** by eliminating outdated and irrelevant content, providing a refined reading experience.

## **Solution Approach**

The News Discovery Agent orchestrates a multi-step, agentic workflow using **LangGraph** to deliver personalized news:

*   **User Verification & Management**: A **SQL agent** is employed to verify user emails and manage preferences. If a user is new, their details (name, email, interests) are collected and stored.
*   **Dynamic Search Query Generation**: Based on a user's interests, the system generates expanded and precise search queries using an **LLM (GPT-4o-mini with low temperature)** to focus on current and trending news.
*   **Real-time News Retrieval**: Utilizes **DuckDuckGo Search (DDGS)** to fetch real-time news articles and links from a wide range of sources.
*   **Intelligent URL Filtering**: An **LLM** is used to filter the retrieved URLs, retaining only those most relevant to the user's specific interests.
*   **Source Credibility Assessment**: URLs are further analyzed by an **LLM** to ensure they come from trustworthy sources, filtering out potentially unreliable or fake news sites.
*   **Advanced Content Processing (Optional)**:
    *   **Web Scraping with BeautifulSoup**: For credible URLs, **BeautifulSoup** is used to scrape and extract the main article content from webpages, stripping away irrelevant elements like scripts and styling.
    *   **LLM-Powered Summarization**: The extracted content is then summarized concisely (e.g., 50 words) by an **LLM** (GPT-4o-mini with high temperature), focusing on the user's interests.
    *   **Grammar and Proofreading**: An **LLM** (GPT-4o-mini with low temperature) performs grammar correction on the summaries to ensure high-quality, readable output.
*   **Personalized Delivery**: Finally, verified, relevant, and optionally summarized news content (URLs and summaries) is delivered to the user.
*   **Deployment**: The entire agent is deployed with **Gradio**, providing an intuitive interface for both existing and new users.

## **Solution Workflow**

(Refer to `flowchart.png` in the notebook for a visual representation of the comprehensive workflow.)

## **Library Installation and LLM Calling**

Install necessary libraries:

```bash
!pip install -q \
  "langchain-core>=0.3.58,<1.0.0" \
  "langchain==0.3.25" \
  "langchain-openai==0.3.35" \
  "langchain-community==0.3.24" \
  "langchain-experimental==0.3.4" \
  "langchain-chroma" \
  "langgraph==0.2.60" \
  "langgraph-prebuilt==0.1.8" \
  "openai" \
  "chromadb" \
  "ddgs"
!pip install gradio -q
```

Initializes OpenAI's GPT-4o-mini model with different temperature settings:

*   **`llm_high (temperature=0.7)`**: Generates more creative and varied responses, used for summarization.
*   **`llm_low (temperature=0)`**: Ensures deterministic and consistent outputs, used for structured tasks like search query expansion, filtering, and grammar correction.

## **Defining the State Schema for LangGraph Workflow**

The `CustomerState` BaseModel establishes a structured state schema to manage data flow across nodes, ensuring seamless transitions and efficient execution within the LangGraph workflow.

## **SQL Agent for Data Retrieval and Customer Information Update**

An AI-powered **SQL agent**, built with **LangChain**, is used for querying and updating the `customer.db` SQLite database, facilitating efficient customer information management. This agent handles user registration, interest storage, and retrieval of existing user data.

## **Customer Email Verification and Data Retrieval**

Functions are implemented for checking existing customer emails in the database. If a user is new, a unique customer ID is generated, and their name and interests are collected and stored. This ensures a personalized experience from the first interaction.

## **Generating Expanded Search Queries for Current News**

Using the `llm_low` (low-temperature) model, precise and time-sensitive search queries are generated based on user interests. This ensures the focus is on breaking news, trending topics, and recent developments, avoiding outdated information.

## **Fetch News Results Using DuckDuckGo**

This component retrieves news results from **DuckDuckGo** based on the expanded search queries. It includes mechanisms for cleaning queries, handling retries, and avoiding blocked sources to ensure a comprehensive and reliable news feed.

## **Filter Relevant URLs Based on User Interests & Trustworthy Sources**

An **LLM** is employed to filter the raw search results. First, it identifies and retains URLs most relevant to the user's specified interests. Second, it assesses the credibility of these news sources, filtering out unreliable or misleading information to ensure the delivery of trustworthy content.

## **LangSmith Tracing for Observability**

**LangSmith** is integrated for comprehensive **observability** of the entire **LangGraph** workflow. This platform is crucial for the development, monitoring, and optimization of this production-grade LLM application.

**Why LangSmith is Used for Observability?**

LangSmith enhances the observability of LLM applications by providing real-time tracking, logging, and monitoring of function executions. This helps developers debug, optimize, and refine their applications efficiently:

1.  **Execution Tracking with Tracing**: Enables detailed tracing of each step within the LangGraph workflow, allowing developers to see how each function executes.
2.  **Structured Logging with RunTree**: Systematically logs function inputs, outputs, execution times, and errors, aiding in pattern identification and debugging.
3.  **Real-Time Monitoring and Insight**: Provides dashboards to track key performance metrics like response times, error rates, and costs.
4.  **Automated Error Handling and Debugging**: Captures detailed error logs and associates them with specific function executions, facilitating quick issue resolution.
5.  **Seamless Syncing and Auditability**: Automatically syncs logs to the platform, providing a complete history of executions for performance improvements and compliance.

By leveraging tracing, structured logging, and real-time monitoring, LangSmith ensures that the News Discovery Agent runs efficiently, reliably, and transparently.

## **Optional Advanced Content: Summarizing and Proofreading**

*   **Web Scraping with BeautifulSoup**: The `summarize_check_site_content` function uses **BeautifulSoup** to effectively parse HTML content from credible URLs. It removes unnecessary elements (like `<script>` and `<style>`) and extracts the main article text, preparing it for further processing.
*   **Text Summarization Function**: Utilizes an **LLM** (`llm_high`) to generate concise, interest-focused summaries of the extracted news content (typically limited to 50 words).
*   **Grammar Correction Using LLM**: Employs an **LLM** (`llm_low`) to check and correct grammatical errors, spelling, and punctuation in the summarized text, ensuring the output is clear, professional, and readable.

## **Deployment with Gradio**

The entire workflow, including user management, news retrieval, filtering, and optional summarization, is deployed using **Gradio**. This provides a user-friendly interface that allows both existing members (by email) and new members (by email, name, and interests) to access personalized news headlines or summaries effortlessly.

## **Summary of Interest-Based News URL Retrieval and Summary Generation Workflow:**

Through a structured approach leveraging **LangChain** and **LangGraph**, we have successfully developed a robust workflow for retrieving, filtering, and refining news content based on user interests. Our key achievements include:

✅ **User Data Retrieval & Onboarding**: Implemented a **SQL agent** for seamless management of user data, including verification for existing users and registration for new members, securely storing their preferences.

✅ **Search Query Expansion**: Employed an **LLM** to generate highly relevant and time-sensitive search queries from user interests, ensuring access to the latest information.

✅ **Reliable Search Integration**: Utilized **DuckDuckGo Search (DDGS)** to fetch unbiased and diverse news sources in real-time.

✅ **Relevance Filtering**: Applied **AI-driven filtering (LLM)** to retain only the URLs that are precisely aligned with user interests.

✅ **Credibility Assessment**: Evaluated news sources using an **LLM** to exclude unreliable or misleading information, ensuring the trustworthiness of all content delivered.

✅ **Web Scraping and Content Extraction**: Integrated **BeautifulSoup** for efficient web scraping to extract meaningful article content from verified URLs.

✅ **LLM-Powered Summarization and Proofreading**: Utilized **LLMs** for generating concise, interest-based summaries and performing grammar correction to enhance readability and quality.

✅ **LangSmith Observability**: Incorporated **LangSmith** for comprehensive tracing, monitoring, and debugging, ensuring the agent's reliability, performance, and transparency in delivering secure, fair, and explainable news recommendations.

✅ **Seamless Deployment**: Successfully deployed the entire workflow using **Gradio**, providing an efficient and intuitive user experience for accessing personalized, trustworthy news URLs and summaries.

At this stage, we have established an efficient, structured, and interest-driven workflow that retrieves, filters, and refines news content, ensuring an optimal and highly personalized user experience.
