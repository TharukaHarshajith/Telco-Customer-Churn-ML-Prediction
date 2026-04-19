# Telco Customer Churn MLOps Project

## Project Overview
This repository contains a complete end-to-end MLOps implementation for predicting customer churn in a telecom business. It includes data preparation, feature engineering, model training, MLflow-based experiment tracking, REST API serving, a web UI, containerization, and deployment automation.

## Core MLOps Components
- Data ingestion and preprocessing pipeline for telecom customer data
- Feature engineering and model training with reproducible experiments
- MLflow tracking for runs, metrics, parameters, and artifacts
- Model serialization and serving with a production-ready FastAPI app
- Web UI integration using Gradio for manual review and demo
- Docker containerization for consistent runtime environments
- CI/CD and deployment guidance for AWS container hosting

## Tools and Technologies Used
- Python 3.x
- pandas, numpy for data ingestion and preprocessing
- scikit-learn for train/test splitting and evaluation workflows
- XGBoost for supervised classification modeling
- MLflow for experiment tracking, model logging, and artifact management
- FastAPI for building the inference REST API
- Gradio for user-facing web UI demonstration
- Docker for container packaging and environment isolation
- AWS ECS Fargate / Application Load Balancer for container deployment (documented architecture)
- GitHub Actions for CI/CD pipeline automation (build + publish Docker image)

## MLOps Workflow
1. Data preparation
   - Load raw telecom customer data
   - Clean and normalize features
   - Convert categorical values to numerical representations
2. Feature engineering
   - Encode binary and categorical columns
   - Create one-hot encoded features for multi-category fields
   - Keep the same feature ordering for training and serving
3. Model training
   - Train an XGBoost classifier on processed customer data
   - Log training runs, metrics, parameters, and artifacts to MLflow
   - Save feature column list and model artifacts for reproducibility
4. Model evaluation
   - Compute precision, recall, F1 score, ROC AUC, and prediction latency
   - Use evaluation results to compare model quality across experiments
5. Model serving
   - Load the trained MLflow model in a FastAPI service
   - Expose a `/predict` endpoint for inference
   - Provide a root health-check endpoint `/`
   - Mount a Gradio UI at `/ui` for manual testing
6. Deployment
   - Build a Docker image with the serving app and dependencies
   - Use CI/CD to ensure build consistency
   - Deploy containerized application to a cloud container service

## Model and Artifact Management
- Model type: XGBoost classifier
- Logged artifacts:
  - `model/` (MLflow pyfunc model)
  - `feature_columns.txt` to enforce consistent feature order at inference time
- Tracking organization:
  - MLflow experiment for run history
  - Metrics for model quality and runtime performance
  - Parameters for hyperparameters and preprocessing decisions

## Important MLOps Considerations
- Reproducibility: All model training runs and artifacts are tracked through MLflow.
- Feature consistency: Serving uses the same feature mapping and column order as training.
- Production readiness: The API is packaged into Docker for consistency between local and deployed environments.
- Observability: Model metrics and experiment history are available via MLflow.
- Deployment readiness: The repo includes container and infrastructure details for launching on AWS.
- Documentation: This file documents the MLOps pipeline, tools, and architecture.

## Key Files and Directories
- `scripts/run_pipeline.py`: Training pipeline and MLflow logging
- `scripts/prepare_processed_data.py`: Data preparation and cleaning
- `src/features/build_features.py`: Feature engineering logic
- `src/models/train.py`: Model training workflow
- `src/serving/inference.py`: Model loading and inference logic
- `src/app/main.py`: FastAPI application entrypoint
- `src/app/app.py`: FastAPI app definition and startup
- `src/utils/validate_data.py`: Data validation utilities
- `dockerfile`: Container definition for app deployment

## Deployment Notes
This project is designed to be packaged into a Docker image, pushed to Docker Hub, and deployed on an AWS server or AWS container service.

### Docker Hub workflow
1. Build the image locally:
```bash
docker build -t yourusername/telco-churn:latest .
```
2. Log in to Docker Hub:
```bash
docker login
```
3. Push the image:
```bash
docker push yourusername/telco-churn:latest
```

### Deploying to an AWS server (EC2)
1. SSH into the AWS server:
```bash
ssh ec2-user@your-aws-server-ip
```
2. Log in to Docker Hub on the server:
```bash
docker login
```
3. Pull the image:
```bash
docker pull yourusername/telco-churn:latest
```
4. Run the container:
```bash
docker run -d --name telco-churn-app -p 8000:8000 yourusername/telco-churn:latest
```
5. Verify the service is running:
```bash
docker ps
curl http://localhost:8000/
```

### Recommended production considerations
- Open port `8000` in the AWS security group to allow external access.
- Use `--restart unless-stopped` for automatic recovery:
```bash
docker run -d --restart unless-stopped --name telco-churn-app -p 8000:8000 yourusername/telco-churn:latest
```
- For AWS ECS/Fargate deployments, the same Docker image can be used in a task definition and service.

## Project Value
This repository demonstrates how to convert a machine learning solution into an operational, observable, and reproducible system. It covers the major phases of MLOps: data, model, deployment, serving, and continuous delivery.
