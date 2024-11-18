# 504_Assignment_Containers

This project involves containerizing a Flask application using Docker and deploying it to **GCP Cloud Run**. Below are the details of the process, including the Dockerfile, deployment steps, screenshots, and reflections.

---

## **1. Dockerfile**
The Dockerfile used to containerize the Flask application is as follows:
```dockerfile
# Use a lightweight Python image as the base
FROM python:3.11-alpine

# Set the working directory
WORKDIR /app

# Copy the application files into the container
COPY . /app

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port the app runs on
EXPOSE 8080

# Define the command to run the app
CMD ["python", "app.py"]
```

---

## **2. Deployment Screenshots**

### **2.1 GCP Cloud Run Deployment**
- **Building the Docker Image in Cloud Shell**:

- **Pushing the Docker Image to Container Registry**:
 
- **Deploying to Cloud Run**:



## **3. Deployed Application URL**: [GCP App Link](https://your-cloud-run-url)


---

## **4. Reflection**

### **Challenges**
1. **Dockerfile Configuration**:
   - Issue: Initial Dockerfile failed due to missing dependencies.
   - Solution: Ensured `requirements.txt` was up-to-date and included all necessary libraries.

2. **GCP Deployment**:
   - Issue: Error while pushing the Docker image to Container Registry.
   - Solution: Used Google Cloud Shell for authentication and proper `gcloud` commands.

### **Lessons Learned**
1. **Docker Fundamentals**: Writing an effective Dockerfile is key to a successful deployment.
2. **Cloud-Specific Features**: GCP has unique configurations that require careful attention to detail.
3. **Automation Tools**: Using tools like Google Cloud Shell streamlined the process significantly.

---

## **5. Repository Structure**
```
flask_app/
├── app.py
├── requirements.txt
├── Dockerfile
├── README.md
└── screenshots/
    ├── gcp_build_image_screenshot.png
    ├── gcp_push_image_screenshot.png
    └── gcp_deploy_screenshot.png
```

---

Let me know if you need help adjusting this further!
