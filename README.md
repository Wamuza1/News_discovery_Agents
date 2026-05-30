# News_discovery_Agents
NewsFindr: AI-Powered Personalized News Discovery Agent

NewsFindr addresses information overload by providing real-time, personalized news updates tailored to user interests. Leveraging LangGraph agentic flow, it ensures accuracy and credibility in recommendations. This project aims to enhance user engagement and optimize content discovery by delivering secure, fair, and explainable news.



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
- Verify User Email: Check if the user's email exists in the database. If invalid, collect and store user details for future use.
- Display User Interests: Retrieve and present user preferences to personalize news recommendations.
- Generate Search Queries: Construct optimized search queries based on user interests to ensure relevant results.
- Retrieve Search Results: Fetch real-time news articles links from multiple trusted sources.
- Extract Relevant Links: Filter and select the most relevant articles aligned with the user’s topics of interest.
- Validate Authentic Sources: Ensure credibility by verifying the source authority and filtering out low-quality or fake news sites.
- Provide Authenticated Links to Users: Deliver only verified and high-quality news links, ensuring reliability and credibility in recommendations.
- Deploy the Agent for Members and New Users: Deploy the AI-powered news retrieval agent accessible to both registered users and new members to generate interest based authenticated news links.

### Optional Advanced Content
- Extract, Summarize, and Proofread Content: Apply NLP techniques to generate concise, accurate summaries while maintaining content integrity.
- Provide Authenticated Links and News Summary to Users: Deliver only verified and high-quality news links, ensuring reliability and credibility in recommendations.
- Deploy the Agent for Members and New Users: Deploy the AI-powered news retrieval agent accessible to both registered users and new members to generate interest based authenticated news links and summary.

## **Solution Workflow**
(Refer to `flowchart.png` in the notebook for a visual representation of the workflow.)

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

Initialize OpenAI's GPT-4o-mini model with different temperature settings for varied and consistent responses.

## **Defining the State Schema for LangGraph Workflow**
The `CustomerState` BaseModel establishes a structured state schema to manage data flow across nodes, ensuring seamless transitions and efficient execution within the LangGraph workflow.

## **SQL Agent for Data Retrieval and Customer Information Update**
An AI-powered SQL agent is used for querying and updating the `customer.db` database, facilitating customer information management.

## **Customer Email Verification and Data Retrieval**
Functions for checking existing customer emails and registering new customers, including generating unique IDs and collecting interests.

## **Generating Expanded Search Queries for Current News**
Using a low-temperature LLM, precise and time-sensitive search queries are generated based on user interests, focusing on current events.

## **Fetch News Results Using DuckDuckGo**
Retrieves news results from DuckDuckGo based on expanded search queries, handling retries and filtering blocked sources.

## **Filter Relevant URLs Based on User Interests & Trustworthy Sources**
Filters search results to retain URLs relevant to user interests and then evaluates the credibility of news sources to filter out unreliable ones.

## **LangSmith Tracing for Observability**
Integrates LangSmith for tracing, monitoring, and logging the execution of the LangGraph workflow, aiding in debugging and performance analysis.

## **Optional Advanced Content: Summarizing and Proofreading**
- **Text Summarization Function**: Generates concise, interest-focused summaries of news content.
- **Grammar Correction Using LLM**: Corrects grammatical errors in the summarized text.
- **Extract and Summarize Website Content**: Retrieves, extracts, summarizes, and proofreads content from credible URLs.

## **Deployment with Gradio**
The entire workflow is deployed using Gradio, providing a user-friendly interface for both existing and new members to access personalized news headlines or summaries.

## **Summary of Interest-Based News Workflow**
This project successfully developed a workflow for retrieving, filtering, and refining news content based on user interests, ensuring an optimal user experience by providing relevant, trustworthy, and grammatically correct news URLs and summaries.
