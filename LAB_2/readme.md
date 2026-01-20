# Cloud Computing Lab 2 – Monolithic Architecture

## Overview
This lab demonstrates the design and limitations of a **monolithic architecture** using a FastAPI-based web application. The application implements multiple features—user login, event listing, checkout, and user-specific event tracking—within a single codebase and deployment unit.

The lab intentionally introduces failures and performance bottlenecks to analyze how monolithic systems behave under errors and load, followed by optimization and performance validation using load testing.

---

## Objectives
- Understand monolithic application architecture
- Observe single point of failure in monolithic systems
- Identify performance bottlenecks in backend routes
- Optimize inefficient backend logic
- Perform load testing and analyze performance improvements

---

## Application Features
- User registration and login
- Event listing
- Event checkout
- My Events dashboard
- HTML-based UI using templates

---

## Routes Optimized

### `/checkout`
- Fixed an intentional crash caused by a division-by-zero error
- Optimized fee calculation logic to reduce unnecessary looping

### `/events`
- Removed an artificial computation loop that caused CPU delay

### `/my-events`
- Removed redundant computation causing artificial delay
- Simplified database query logic for better performance

---

## Performance Testing
Load testing was performed using **Locust** to simulate concurrent users and evaluate:
- Average response time
- Request throughput
- System behavior before and after optimization

Performance improvements were observed after removing inefficient logic and optimizing backend routes.

---

## Technologies Used
- Python
- FastAPI
- SQLite
- Locust
- HTML (Jinja Templates)

---

## Folder Structure
```text
CC_LAB2/
├── main.py
├── checkout/
├── events/
├── my_events/
├── locust/
├── templates/
├── requirements.txt
└── insert_events.py
