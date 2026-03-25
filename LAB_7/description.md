# Cloud Computing Lab 7

## MinIO and Ceph Storage

---

## Aim

To understand and implement **Block Storage (Ceph)** and **Object Storage (MinIO)**, and analyze their behavior through practical experiments.

---

## Technologies Used

* Docker & Docker Compose
* Flask (Python)
* MinIO (Object Storage)
* SQLite (Block Storage simulation)

---

## 🚀 Setup and Execution

### 1. Folder Setup

* Created a folder with SRN
* Extracted lab files inside it

---

### 2. Modify Bucket Name

* Opened `app.py`
* Updated bucket name to SRN

---

### 3. Run Docker Containers

```bash
docker-compose up --build
```

---

### 4. Verify Services

* Flask App → http://localhost:5000
* MinIO Dashboard → http://localhost:9001

Login Credentials:

* Username: `admin_user`
* Password: `admin_password`

---

### 5. Upload Image

```bash
curl.exe -X POST -F "name=Phone" -F "price=500" -F "image=@\"C:\path\to\image.jpg\"" http://localhost:5000/product
```

---

## Observations

### Object Storage (MinIO)

* Image successfully uploaded
* Accessible via MinIO dashboard

### Block Storage (Database)

* `ecommerce.db` file created
* Stores structured data (name, price, image name)
* Image file not stored locally

---

## Experiment 1: Access Method

### Observation:

* Database visible locally
* Image only available in MinIO

### Conclusion:

* Block storage behaves like disk
* Object storage is accessed via API

---

## 🧪 Experiment 2: Metadata

### Implementation:

```python
file_metadata = {
    "x-amz-meta-product-name": str(name),
    "x-amz-meta-product-price": str(price)
}
```

### Observation:

* Metadata visible in MinIO UI
* No need to open file

### Conclusion:

* Object storage supports metadata
* Block storage does not

---

## Experiment 3: Scaling

### Observation:

* Block storage limited by disk size
* MinIO continues to accept uploads

### Conclusion:

* Object storage scales horizontally
* Block storage has fixed capacity

---

## Experiment 4: Failure Testing

### Steps:

* Stopped MinIO → Image upload failed
* Stopped Webapp → Data persisted

### Conclusion:

* Storage and application are independent
* Data persists even if service is down

---

## Conclusion

This lab demonstrated the difference between **block storage and object storage**.

* Block storage is suitable for structured data
* Object storage is ideal for unstructured data
* Metadata and scalability are key advantages of object storage

---

## Student Details

* **Name:** Vardha Kathuria
* **SRN:** PES1UG23AM343
* **Section:** F

---
