#  AWS AI Customer Support Chatbot

An intelligent, multi-turn customer support agent built using **Amazon Bedrock Flows**, **AWS Lambda**, and **DynamoDB**. This project demonstrates how to build production-ready, agentic AI applications that can route user intents, ground responses in company data to prevent hallucinations, and execute real-world actions like creating database tickets.

## 🌟 Key Features

- **Intelligent Intent Routing:** Automatically classifies incoming messages into three distinct paths: Bug Reports, Platform FAQs, or Out-of-Scope requests.
- **Agentic Tool Use:** For bug reports, the AI engages in multi-turn conversation to gather missing details (description, steps to reproduce, environment) and autonomously calls an AWS Lambda function to persist the ticket in DynamoDB.
- **Grounded FAQ Responses:** Answers platform questions strictly using an embedded company FAQ, eliminating AI hallucinations.
- **Automated LLM-as-a-Judge Testing:** Includes a custom Python evaluation harness that generates test datasets and leverages **Amazon Bedrock Evaluations** to automatically grade the chatbot's correctness.
- **Infrastructure as Code (IaC):** Backend resources (DynamoDB, Lambda, IAM roles, S3) are deployed securely using AWS CloudFormation.

##  Architecture & How It Works

The application is built on the **Amazon Bedrock Flows** visual builder, which orchestrates the AI agent loop:

1. **Input Node:** Receives the user's text prompt.
2. **Classifier Node (Prompt):** Uses Amazon Nova Pro to analyze the text and output a strict category (`BUG`, `FAQ`, or `OTHER`).
3. **Router Node (Condition):** Routes the flow based on the classifier's output.
4. **Execution Paths:**
   - **Bug Path:** A prompt node instructs the AI to collect missing bug details. Once gathered, it triggers a tool call to invoke a **Lambda function**, which writes the ticket to **DynamoDB**.
   - **FAQ Path:** A prompt node containing the full company FAQ grounds the AI's response.
   - **Handoff Path:** Politely redirects out-of-scope queries to a human support phone line.
5. **Output Node:** Returns the final generated response to the user.

##  Tech Stack

- **Cloud & AI:** Amazon Bedrock Flows, Amazon Nova Pro (Foundation Model), Amazon Bedrock Evaluations
- **Compute & Database:** AWS Lambda (Python 3.12), Amazon DynamoDB
- **Infrastructure:** AWS CloudFormation, IAM (Role-based access control)
- **Languages & Tools:** Python 3.9+, Boto3, AWS CLI

---

##  Getting Started

### Prerequisites
Before you begin, ensure you have the following:
- An active **AWS Account** with access to Amazon Bedrock (specifically the `us-east-1` region).
- **AWS CLI** installed and configured with your credentials (`aws configure`).
- **Python 3.9+** installed on your machine.
- A foundational understanding of AWS IAM and basic Python.

### 1. Clone the Repository
```bash
git clone https://github.com/prod0008/aws-customer-support-chatbot.git
cd aws-customer-support-chatbot/project/starter
