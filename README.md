# HHA504 Assignment: Deploying and Managing Containers

## Overview
This project demonstrates how to containerize a Python Flask application, deploy it to Google Cloud Run, and reflect on the process.

---

## 1. Creating the Flask Application Using Google Cloud Shell

### 1.1 Writing the Application Code
 The following code was saved in `app.py`:

```python
from flask import Flask, url_for

app = Flask(__name__)

@app.route("/")
def home():
    image_url = url_for('static', filename='images/cat.jpg')
    print(f"Image URL: {image_url}")
    return f"""
    <html>
        <head><title>Flask App with Image</title></head>
        <body>
            <h1>Welcome to My Flask App!</h1>
            <img src="{image_url}" alt="Example Image" style="width:300px;height:auto;">
        </body>
    </html>
    """

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```
 
## 2. Dockerfile

```dockerfile
# Use the official Python image
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy all application files into the container
COPY . /app

# Install Flask
RUN pip install flask

# Expose port 8080 for Flask
EXPOSE 8080

# Run the Flask app
CMD ["python", "app.py"]
```
---

## 3. Deployment Process

### 3.1 Steps to Containerize the Application
 1. Created a simple Python Flask application with the following structure:

```my_flask_app
my_flask_app/
├── app.py
├── Dockerfile
└── static/
    └── images/
        └── cat.jpg
```
 2. Built the Docker image locally:
    ```
    docker build -t gcp-flask-app .
    ```
 3. Tested the application locally:
    ```
    docker run -p 9090:8080 gcp-flask-app
    ```
#### Screenshots:

![image](https://github.com/user-attachments/assets/00667e14-eb0f-4f35-b4cb-2018be15b842)

---
    
![image](https://github.com/user-attachments/assets/f41bf8f8-dda7-41f8-a801-7d62230d256f)

---

### 3.2 Push Docker Image to Google Container Registry (GCR)
 1. Tagged the Docker image:
    ```
    docker tag gcp-flask-app gcr.io/cain-samantha-hha504/gcp-flask-app
    ```
 2. Pushed the image to GCR:
    ```
    docker push gcr.io/cain-samantha-hha504/gcp-flask-app
    ```
### 3.3 Deploy to Google Cloud Run
 1. Deployed the containerized application:
    ```
    gcloud run deploy gcp-flask-app \
      --image gcr.io/cain-samantha-hha504/gcp-flask-app \
      --platform managed \
      --region us-central1 \
      --allow-unauthenticated
    ```
 2. Verified deployment using the provided URL:
     Deployed URL: https://gcp-flask-app-829081573209.us-central1.run.app

#### Screenshots: 

![image](https://github.com/user-attachments/assets/d67db1cd-f4de-4623-baa6-f5c43b9bfb7f)

---
![image](https://github.com/user-attachments/assets/d6964373-f32a-4482-b580-e9c1e401f683)

---

## 4. Reflection

### Challenges Faced:
 - Port Binding Error: Encountered a port conflict when running the Docker container locally. Resolved by using a different port (9090).
 - Project Configuration Error: Initially, Cloud Run deployment failed due to the project not being specified in gcloud. Fixed by setting the project using gcloud config set project.



