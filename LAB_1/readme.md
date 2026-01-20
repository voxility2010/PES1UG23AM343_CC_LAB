# Cloud Computing Lab 1 – Cloud Service Models (IAAS, PAAS, SAAS)

## Overview
This lab introduces fundamental cloud computing service models through hands-on implementation. The experiment demonstrates the practical usage of **Infrastructure as a Service (IAAS)**, **Platform as a Service (PAAS)**, and **Software as a Service (SAAS)** using real cloud platforms and tools.

The lab is divided into three parts:
- Object Storage using Supabase (IAAS)
- Serverless Functions using Napkin (PAAS)
- Application Deployment using GitHub and Vercel (SAAS)

---

## Objectives
- Understand core cloud computing concepts
- Work with object storage services
- Deploy serverless functions
- Host and deploy a static web application
- Gain practical exposure to real-world cloud platforms

---

## Part A: IAAS – Object Storage using Supabase
- Created a Supabase project using free tier
- Enabled storage access policies using SQL Editor
- Created a public storage bucket using Python SDK
- Uploaded an image to the bucket programmatically
- Generated a public URL for the uploaded object

This part demonstrates how cloud providers offer scalable infrastructure for storage without managing physical hardware.

---

## Part B: PAAS – Function as a Service using Napkin
- Created a workspace on Napkin platform
- Developed a serverless Python function
- Implemented a simple joke generator API
- Deployed the function directly from the browser
- Accessed the function using a public URL

This part illustrates how PAAS abstracts infrastructure management and allows developers to deploy individual functions easily.

---

## Part C: SAAS – Application Deployment using Vercel
- Customized a portfolio website using HTML
- Hosted the source code on a public GitHub repository
- Deployed the application using Vercel
- Accessed the deployed website using a public URL

This section demonstrates how complete software applications can be delivered to users as a service.

---

## Technologies Used
- Python
- Supabase (Object Storage)
- Napkin (Serverless Functions)
- GitHub
- Vercel
- HTML

---

## Repository Structure
```text
CC_LAB1/
├── supabase_object_store.py
├── function_as_a_service.py
├── portfolio-template/
│   └── index.html
└── README.md
