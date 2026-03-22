# Aws-AI-Assistant

# 🚀 AWS AI Assistant (Bedrock Agent Powered)

An AI-powered AWS assistant built using **Amazon Bedrock, Lambda, API Gateway, and S3** to intelligently discover, analyze, and manage AWS resources with a safe, confirmation-based workflow.

---

## 🧠 Overview

This project solves a real-world cloud problem:

- Unused AWS resources increase costs silently  
- Manual monitoring is time-consuming  
- Beginners don’t know what is safe to delete  

👉 This AI assistant:
- Detects chargeable resources  
- Explains them in simple language  
- Recommends cleanup actions  
- Executes deletion **only after user confirmation**

---

## ⚙️ Architecture


User (Browser)
↓
S3 Static Website (Frontend UI)
↓
API Gateway (/chat)
↓
Lambda (BedrockAgentChatProxy)
↓
Bedrock Agent (Ritik-AWS-Admin-Agent)
↓
Action Group (CostCleanupTools)
↓
Lambda (BedrockCostAgentTools)
↓
AWS Services (EC2, EBS, EIP)


---

## 🧰 AWS Services Used

- Amazon Bedrock (Agent + Nova Pro model)
- AWS Lambda (2 functions)
- Amazon API Gateway (HTTP API)
- Amazon S3 (Static website hosting)
- IAM (Roles & Policies)
- CloudWatch (Logging)

---

## 🔐 IAM Roles

### 1. BedrockCostAgentLambdaRole
Used by Lambda (**BedrockCostAgentTools**) to interact with AWS resources.

Permissions:
- EC2 (Describe, Release Elastic IP)
- EBS (Describe, Delete Snapshot)
- CloudWatch Logs

---

### 2. BedrockAgentChatProxyRole
Used by Lambda (**BedrockAgentChatProxy**) to invoke Bedrock Agent.

Permissions:
- `bedrock:InvokeAgent`
- CloudWatch Logs

---

## ⚙️ Lambda Functions

### 1. BedrockCostAgentTools
Handles AWS operations:
- `discover_cost_resources`
- `delete_cost_resource`

---

### 2. BedrockAgentChatProxy
Acts as backend bridge:
- Accepts user request
- Calls Bedrock Agent
- Returns response

---

## 🔗 API Gateway

- API Name: `Chat-Integration`
- Route:

POST /chat


💻 Frontend
Built using HTML, CSS, JavaScript
Hosted on S3 (Static Website)
API Integration
const API_URL = "https://<api-id>.execute-api.ap-south-1.amazonaws.com/chat";



🔐 Safety Mechanism

The system follows a strict workflow:

Detect → Explain → Recommend → Confirm → Act
No resource is deleted automatically
User must type: CONFIRM
Only selected resource is deleted



🧪 Testing
Test 1 — Discovery
Find chargeable resources in ap-south-1
Test 2 — Delete Request
Delete EIP eipalloc-xxxx
Test 3 — Confirmation
CONFIRM



🎯 Features
AI-powered AWS resource analysis
Cost optimization recommendations
Safe deletion workflow
Fully serverless architecture
Real-time chat interface



🚀 Future Improvements
Multi-region support
Scheduled automatic cleanup
Slack / WhatsApp integration
Dashboard for cost insights



🧠 Key Learning
Built real-world AI + Cloud integration
Used Bedrock Agents with Action Groups
Implemented secure serverless architecture



📌 One-Line Summary

Built a serverless AI assistant using Amazon Bedrock, Lambda, API Gateway, and S3 to automate AWS cost optimization with a secure confirmation-based workflow.

🛡️ Ensures safe and controlled automation

💥 Summary

This project brings together AI + AWS + Automation to create a smart assistant that not only saves cost but also improves decision-making, learning, and operational efficiency.


👨‍💻 Author

Ritik Mohadikar
AWS Cloud Engineer
