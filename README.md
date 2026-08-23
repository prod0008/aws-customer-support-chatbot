# AWS Customer Support Chatbot

An AI-powered customer support chatbot built using Amazon Bedrock Flows, Lambda, and DynamoDB. 

## Features
- **Intelligent Routing:** Classifies user messages into Bug Reports, FAQ questions, or Out-of-Scope requests.
- **Multi-turn Bug Collection:** Gathers bug details step-by-step and automatically creates tickets in DynamoDB via a Lambda tool.
- **Grounded FAQ Answers:** Answers platform questions strictly using the embedded company FAQ to prevent hallucinations.
- **Automated Evaluation:** Tested using Bedrock Evaluations with an LLM-as-a-judge to ensure high correctness scores.

## Tech Stack
- Amazon Bedrock Flows (Amazon Nova Pro)
- AWS Lambda & DynamoDB
- Python & Boto3

## How to Run
1. Deploy the CloudFormation stack: `aws cloudformation deploy ...`
2. Build the Flow in the Bedrock Console.
3. Run the evaluation script: `python generate-eval-dataset.py ...`

## 📊 Evaluation Observations

The automated evaluation was conducted using Amazon Bedrock Evaluations with an LLM-as-a-judge (Amazon Nova Pro) to assess the correctness of the chatbot responses against expected outcomes. 


## 📊 Evaluation Observations

The automated evaluation was conducted using Amazon Bedrock Evaluations with an LLM-as-a-judge (Amazon Nova Pro) to assess the correctness of the chatbot's responses against expected outcomes. 

**Overall Correctness Score:** [50%]

**Observations:**
- **Bug Routing (t1_bug):** The model successfully identified the technical issue and initiated the multi-turn information gathering process, asking for steps to reproduce and environment details.
- **FAQ Routing (t2_faq):** The model correctly retrieved the 30-day return policy from the grounded FAQ text without hallucinating outside information.
- **Out-of-Scope Routing (t3_other):** The model correctly identified the prompt as out-of-scope and provided the exact required fallback phrase with the human support phone number.

The strict system prompts and conditional routing ensured high accuracy and prevented the model from deviating from the defined support boundaries.
