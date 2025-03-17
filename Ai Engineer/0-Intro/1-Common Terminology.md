# **AI Terminologies**

## **AI vs AGI**

| **Aspect**       | **AI (Artificial Intelligence)**                              | **AGI (Artificial General Intelligence)**             |
| ---------------- | ------------------------------------------------------------- | ----------------------------------------------------- |
| **Definition**   | Task-specific intelligence (e.g., chatbots, recommendations). | Hypothetical AI with human-like learning & reasoning. |
| **Scope**        | Narrow, specialized applications.                             | Broad, adaptable across various domains.              |
| **Capabilities** | Performs only trained tasks.                                  | Learns and reasons autonomously.                      |
| **Examples**     | Siri, Alexa, recommendation systems.                          | Exists only in theory, seen in sci-fi.                |
| **Status**       | Widely used in industries.                                    | No real-world AGI yet.                                |

---

## **Large Language Models (LLMs)**

AI models trained on vast datasets to process and generate human-like text.

### **Key Features**

- **Trained on Massive Data** – Books, articles, websites.
- **Uses Deep Learning** – Transformers for context understanding.
- **Applications** – Chatbots, translation, coding assistance.

### **Challenges**

- **Bias & Ethics** – Risk of reinforcing biases in training data.
- **Computational Costs** – Requires powerful infrastructure.
- **Security Risks** – Susceptible to manipulation.

---

## **AI Training vs. Inference**

### **Training**

- Model learns patterns from data.
- Requires large computational resources.
- Example: Teaching AI to recognize traffic signs.

### **Inference**

- AI makes predictions based on training.
- Requires less computation.
- Example: Self-driving cars detecting stop signs.

---

## **Embeddings & Vector Databases**

### **Embeddings**

Convert real-world data (text, images, audio) into numerical representations for AI processing.

### **Vector Databases**

Store and query embeddings for efficient similarity searches.

### **Use Cases**

- **Semantic Search** – Finding contextually relevant content.
- **Recommendation Engines** – Suggesting similar items.
- **Anomaly Detection** – Identifying outliers in data.
- **RAG for LLMs** – Enhancing AI responses with external knowledge.

### **Vector Search Process**

1. **Generate Embeddings** – Convert data into vectors.
2. **Indexing** – Store embeddings for fast retrieval.
3. **Query Embedding** – Convert search input into a vector.
4. **Similarity Search** – Retrieve relevant results.

---

## **AI Agents**

AI agents are autonomous systems that **perceive, reason, and act** to achieve goals. They interact with their environment, make decisions, and improve over time.

### **Types**

- **Reactive** – Respond to stimuli without memory.
- **Model-Based** – Use internal knowledge for decisions.
- **Goal-Based** – Plan actions to achieve objectives.
- **Learning** – Adapt using machine learning.

### **How They Work**

1. **Receive Input** → Process data from users or the environment.
2. **Decision-Making** → Analyze and select the best action.
3. **Execute Action** → Perform tasks autonomously.
4. **Learn & Adapt** → Improve through feedback.

### **Applications**

- **Chatbots** – AI-driven assistants (e.g., ChatGPT).
- **Autonomous Vehicles** – Self-driving decision-making.
- **Cybersecurity** – Detecting and responding to threats.
- **Automated Research** – Fetching and summarizing data.

---

## **Retrieval-Augmented Generation (RAG)**

Enhances **LLM responses** by retrieving real-time external knowledge before generating answers.

### **How It Works**

1. **Query** → LLM receives input.
2. **Retrieval** → Searches external data sources.
3. **Augmentation** → Injects retrieved data into the prompt.
4. **Generation** → Produces a well-informed response.

### **Benefits**

- **Improved Accuracy** – Reduces AI hallucinations.
- **Up-to-Date Information** – Uses current knowledge.
- **Efficient Learning** – No need to retrain the model.

### **Use Cases**

- **Enterprise Chatbots** – Answering queries from company data.
- **Research Assistants** – Summarizing academic papers.
- **Legal & Compliance** – Providing accurate legal references.

---

## **Prompt Engineering**

Optimizing AI inputs for better performance and relevance.

### **Key Techniques**

1. **Be Clear & Specific** – Use direct instructions.
2. **Role-Based Prompts** – Assign AI a persona (_"Act as a cybersecurity expert."_)
3. **Step-by-Step Guidance** – Encourage structured responses.
4. **Use Constraints** – Set limits (e.g., _"Summarize in 100 words."_)
5. **Examples & Formatting** – Provide templates for consistency.

### **Advanced Strategies**

- **Few-Shot Prompting** – Guide AI with multiple examples.
- **Chain-of-Thought** – Encourage reasoning (_"Think step by step."_)
- **System Messages** – Control AI behavior in structured interactions.

### **Applications**

- **Customer Support** – Context-aware responses.
- **Content Generation** – Summarization & SEO optimization.
- **Code Assistance** – Debugging & explanations.
