

---

# 🚀 Customer Retention Prediction System

> A production-ready **Machine Learning system** to predict telecom customer churn and enable data-driven retention strategies.

---

## 🎯 Purpose

Customer churn is a major challenge in the telecom industry.
This project helps businesses:

* 🔍 Identify customers **likely to leave**
* 📊 Understand **key churn drivers**
* 🎯 Take **proactive retention actions**
* 💡 Improve **customer lifetime value**

---

## 🧠 Solution Overview

This system delivers an **end-to-end ML pipeline** — from raw data to real-time predictions:

```
Raw Data → Preprocessing → Feature Engineering → Model Training → API → Deployment
```

✔ Predicts churn probability using historical customer data
✔ Provides both **API access** and **interactive UI**
✔ Fully **containerized and cloud-deployable**

---

## ⚙️ Tech Stack

### 🧪 Machine Learning

* **XGBoost** – High-performance classification model
* **Scikit-learn** – Data preprocessing & evaluation
* **Pandas & NumPy** – Data manipulation

### 📊 MLOps & Experiment Tracking

* **MLflow** – Experiment tracking & model versioning

### 🌐 Backend & Serving

* **FastAPI** – High-performance REST API
* **Pydantic** – Data validation

### 🖥️ Frontend / UI

* **Gradio** – Interactive web interface

### 🐳 DevOps & Deployment

* **Docker** – Containerization
* **GitHub Actions** – CI/CD automation
* **AWS ECS Fargate** – Serverless container deployment
* **Application Load Balancer (ALB)** – Traffic routing

---

## 🏗️ System Architecture

### 🔄 ML Pipeline

1. Data preprocessing & cleaning
2. Feature engineering
3. Model training (XGBoost)
4. Evaluation & logging (MLflow)

### 🚀 Serving Layer

* REST API via FastAPI
* Web UI via Gradio

### ☁️ Deployment

* Dockerized application
* Deployed on AWS ECS Fargate

---

## 📡 API Endpoints

| Method | Endpoint   | Description       |
| ------ | ---------- | ----------------- |
| GET    | `/health`  | Health check      |
| POST   | `/predict` | Predict churn     |
| GET    | `/ui`      | Web interface     |
| GET    | `/docs`    | API documentation |

---

## ⚡ Quick Start

### 🖥️ Run Locally

```bash
git clone <repository-url>
cd Telco-Customer-Churn-ML
pip install -r requirements.txt
```

### ▶️ Train Model

```bash
python scripts/run_pipeline.py \
  --input data/raw/Telco-Customer-Churn.csv \
  --target Churn
```

### 🌐 Start Server

```bash
python -m uvicorn src.app.main:app --host 0.0.0.0 --port 8000
```

### 🔗 Access

* UI → [http://localhost:8000/ui](http://localhost:8000/ui)
* Docs → [http://localhost:8000/docs](http://localhost:8000/docs)
* Health → [http://localhost:8000/health](http://localhost:8000/health)

---

## 🐳 Docker Deployment

```bash
docker build -t churn-prediction-app .
docker run -p 8000:8000 churn-prediction-app
```

---

## 📊 Example API Request

```python
import requests

data = {
    "gender": "Female",
    "Partner": "No",
    "Dependents": "No",
    "PhoneService": "Yes",
    "MultipleLines": "No",
    "InternetService": "Fiber optic",
    "OnlineSecurity": "No",
    "OnlineBackup": "No",
    "DeviceProtection": "No",
    "TechSupport": "No",
    "StreamingTV": "Yes",
    "StreamingMovies": "Yes",
    "Contract": "Month-to-month",
    "PaperlessBilling": "Yes",
    "PaymentMethod": "Electronic check",
    "tenure": 1,
    "MonthlyCharges": 85.0,
    "TotalCharges": 85.0
}

response = requests.post("http://localhost:8000/predict", json=data)
print(response.json())
```

---

## 📈 Key Insights from Model

* 📅 **Contract Type** → Month-to-month users churn more
* 🌐 **Internet Service** → Fiber users show higher churn
* 💳 **Payment Method** → Electronic check users at risk
* ⏳ **Tenure** → New customers more likely to leave
* 🔒 **Service Add-ons** → Lack of support increases churn

---

## 📂 Project Structure

```
├── data/
├── mlruns/
├── scripts/
├── src/
├── artifacts/
├── Dockerfile
└── requirements.txt
```

---

## 🔁 CI/CD Pipeline

* Triggered on push to `main`
* Builds Docker image
* Pushes to Docker Hub
* Deploys to AWS ECS (optional)

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch
3. Make changes
4. Run tests
5. Submit PR

---

## 📄 License

MIT License

---

## ⭐ Why This Project Stands Out

* ✅ End-to-end ML system (not just a notebook)
* ✅ Production-ready architecture
* ✅ Real-time prediction API
* ✅ Cloud deployment (AWS)
* ✅ Strong MLOps practices

---

If you want, I can also:

* Add **badges (GitHub, Docker, MLflow, AWS)**
* Create a **README banner image**
* Or tailor this specifically for **GitHub portfolio / recruiters**
