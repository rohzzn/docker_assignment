# Docker Assignment: End-to-End Container Automation

## Introduction

This project involves creating an end-to-end Docker container that automates the process of reading text files, processing data, and generating output. The container runs a Python script that reads two text files, performs text analysis, and outputs the results.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Build the Docker Image](#2-build-the-docker-image)
  - [3. Run the Docker Container](#3-run-the-docker-container)
- [Script Overview](#script-overview)
- [Expected Output](#expected-output)
- [Optimizing the Docker Image](#optimizing-the-docker-image)
- [Extra Credit: Kubernetes Deployment](#extra-credit-kubernetes-deployment)
- [Files to Submit](#files-to-submit)
- [License](#license)

## Prerequisites

- Docker Desktop installed on your personal computer (Windows, macOS, or Linux).
- Basic knowledge of Docker and Python programming.
- Optional: Kubernetes enabled in Docker Desktop for extra credit.

## Project Structure

```
docker_assignment/
├── data/
│   ├── AlwaysRememberUsThisWay.txt
│   ├── IF.txt
│   └── output/            # Output directory (created by the script)
├── script.py              # Python script to process the text files
├── Dockerfile             # Dockerfile to build the Docker image
└── README.md              # Project documentation
```

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your_username/docker_assignment.git
cd docker_assignment
```

### 2. Build the Docker Image

Replace `your_email_username` with your actual email username.

```bash
docker build -t your_email_username .
```

Example:

```bash
docker build -t KANSKRI .
```

### 3. Run the Docker Container

```bash
docker run --rm your_email_username
```

Example:

```bash
docker run --rm KANSKRI
```

The `--rm` flag ensures that the container is removed after it exits.

## Script Overview

The `script.py` performs the following tasks:

1. **Reads two text files** located at `/home/data` inside the container:
   - `IF.txt`
   - `AlwaysRememberUsThisWay.txt`

2. **Counts the total number of words** in each text file.

3. **Calculates the grand total of words** across both files.

4. **Identifies the top 3 most frequent words** and their counts in `IF.txt`.

5. **Handles contractions** in `AlwaysRememberUsThisWay.txt` by splitting them and finds the top 3 most frequent words.

6. **Determines the IP address** of the machine running the container.

7. **Writes the results to a text file** at `/home/data/output/result.txt`.

8. **Prints the contents of `result.txt` to the console** before exiting.

## Expected Output

When you run the container, you should see output similar to the following:

```
Total words in IF.txt: 270
Total words in AlwaysRememberUsThisWay.txt: 222
Grand total of words: 492

Top 3 words in IF.txt:
- you: 29
- and: 22
- if: 16

Top 3 words in AlwaysRememberUsThisWay.txt:
- i: 16
- the: 15
- and: 12

IP Address of the machine running the container: [IP_ADDRESS]
```

*Note:* `[IP_ADDRESS]` will be replaced with the actual IP address when the container runs.

## Optimizing the Docker Image

To ensure the Docker image size is as small as possible (target size: less than 200MB):

- Use a lightweight base image: `python:3.9-slim`.
- Avoid installing unnecessary packages.
- Copy only the necessary files into the image.

Check the image size using:

```bash
docker images
```

## Extra Credit: Kubernetes Deployment

### 1. Enable Kubernetes in Docker Desktop

- Open Docker Desktop.
- Go to **Settings** > **Kubernetes**.
- Enable Kubernetes and apply changes.

### 2. Create Kubernetes Deployment

Create a `deployment.yaml` file:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: docker-assignment-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: docker-assignment
  template:
    metadata:
      labels:
        app: docker-assignment
    spec:
      containers:
      - name: docker-assignment-container
        image: your_email_username
        imagePullPolicy: IfNotPresent
```

### 3. Apply the Deployment

```bash
kubectl apply -f deployment.yaml
```

### 4. Verify the Pods

```bash
kubectl get pods
```

Save the output:

```bash
kubectl get pods > kube_output.txt
```

### 5. Monitor the Pods

To view logs from the pods:

```bash
kubectl logs -f [pod-name]
```

Replace `[pod-name]` with the name of the pod.

### 6. Clean Up

Delete the deployment:

```bash
kubectl delete deployment docker-assignment-deployment
```
