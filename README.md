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
