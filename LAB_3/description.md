# [cite_start]Cloud Computing Lab-3: Spam Detection using ML (Dockerized) [cite: 1, 84]

## 📌 Overview
[cite_start]This project is a Machine Learning-based Spam Detection web application designed to classify messages as "SPAM" or "NOT SPAM"[cite: 84, 87, 92]. [cite_start]The application is built using Python and is fully containerized using Docker to ensure consistent deployment[cite: 46, 62, 84].

## 🧑‍🎓 Student Details
* [cite_start]**Name:** Vardha Kathuria / PES1UG23MA343 [cite: 2, 78]
* [cite_start]**SRN:** PES1UG23AM343 [cite: 3]
* [cite_start]**Section:** F [cite: 2]

## 📁 Project Structure
[cite_start]The Docker image is built using the following core files and directories[cite: 62]:
* [cite_start]`app.py`: The main Flask application script[cite: 62].
* [cite_start]`spam classifier_model.pkl`: The pre-trained machine learning model[cite: 62].
* [cite_start]`tfidf_vectorizer.pkl`: The TF-IDF vectorizer for text processing[cite: 62].
* [cite_start]`templates/`: Directory containing the web application's HTML templates[cite: 62].

## 🛠️ Technologies Used
* [cite_start]**Base Image:** `python:3.10-slim` [cite: 46]
* [cite_start]**Python Packages:** `Flask`, `scikit-learn`, `joblib` [cite: 62]

## 🚀 Local Setup & Execution

### 1. Build the Docker Image
[cite_start]Navigate to your project directory and build the Docker image using the provided `Dockerfile`[cite: 61, 62]:
```bash
docker build -t spam-web-app-pes1ug23am343 .
