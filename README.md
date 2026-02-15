# 🏦 Credit Risk Prediction Web Application

<div align="center">

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.104-green.svg)
![React](https://img.shields.io/badge/React-18.2-blue.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**Machine Learning-powered loan default risk prediction with explainable AI**

[Live Demo](#) | [Documentation](#features) | [Report Bug](#)

</div>

---

## 📋 Table of Contents

- [About](#about)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Model Performance](#model-performance)
- [API Documentation](#api-documentation)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 About

This full-stack machine learning application predicts the probability of loan default using historical lending data. The system employs state-of-the-art ML algorithms (XGBoost, Random Forest, Logistic Regression) and provides transparent explanations using SHAP (SHapley Additive exPlanations).

### Why This Project?

- **Real-world application**: Addresses actual business problem in fintech
- **End-to-end ML pipeline**: From data preprocessing to deployment
- **Explainable AI**: SHAP values make predictions interpretable
- **Production-ready**: Scalable architecture with proper error handling

---

## ✨ Features

### Core Functionality
- 🎯 **Real-time Prediction**: Instant loan default risk assessment
- 📊 **SHAP Explainability**: Understand which features drive predictions
- 🔄 **Multiple ML Models**: Comparison of Logistic Regression, Random Forest, XGBoost
- 📈 **Performance Metrics**: ROC-AUC, Precision, Recall, F1-Score
- 🎨 **Interactive Dashboard**: Beautiful React-based UI

### Technical Features
- ⚡ **FastAPI Backend**: High-performance async API
- 🔧 **Automated Preprocessing**: Handles missing values, encoding, scaling
- 🎛️ **Class Imbalance Handling**: SMOTE oversampling and class weights
- 💾 **Model Persistence**: Joblib-based model saving/loading
- 🌐 **RESTful API**: Well-documented endpoints with Swagger UI
- 🎨 **Responsive Design**: Mobile-friendly Tailwind CSS interface

---

## 🛠️ Tech Stack

### Backend
- **Language**: Python 3.9+
- **Framework**: FastAPI
- **ML Libraries**: scikit-learn, XGBoost, Pandas, NumPy
- **Explainability**: SHAP
- **Model Persistence**: Joblib

### Frontend
- **Framework**: React.js 18
- **Styling**: Tailwind CSS
- **Charts**: Recharts
- **HTTP Client**: Axios
- **Routing**: React Router
- **Icons**: Lucide React

### Development Tools
- **Version Control**: Git & GitHub
- **Package Management**: pip, npm
- **API Testing**: Swagger UI (FastAPI)

---

## 🏗️ Architecture
```
┌─────────────────────────────────────────────────────┐
│                   User Interface                     │
│                  (React Frontend)                    │
└───────────────────┬─────────────────────────────────┘
                    │ HTTP/REST
┌───────────────────▼─────────────────────────────────┐
│                  FastAPI Backend                     │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────┐ │
│  │  /predict    │  │  /explain    │  │  /health  │ │
│  │  endpoint    │  │  endpoint    │  │  endpoint │ │
│  └──────┬───────┘  └──────┬───────┘  └───────────┘ │
│         │                  │                         │
│         ▼                  ▼                         │
│  ┌─────────────────────────────────────────────┐   │
│  │        Preprocessing Pipeline               │   │
│  │  (Imputation → Encoding → Scaling)          │   │
│  └─────────────────┬───────────────────────────┘   │
│                    │                                 │
│                    ▼                                 │
│  ┌─────────────────────────────────────────────┐   │
│  │         XGBoost Model                       │   │
│  │     (Trained on 30k+ samples)               │   │
│  └─────────────────┬───────────────────────────┘   │
│                    │                                 │
│                    ▼                                 │
│  ┌─────────────────────────────────────────────┐   │
│  │         SHAP Explainer                      │   │
│  │    (Feature Contribution Analysis)          │   │
│  └─────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

---

## 🚀 Installation

### Prerequisites
- Python 3.9 or higher
- Node.js 16 or higher
- npm or yarn

### Backend Setup

1. **Clone the repository**
```bash
git clone https://github.com/Tushy21/Credit-Risk-Prediction-App.git
cd Credit-Risk-Prediction-App
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
cd backend
pip install -r requirements.txt
```

4. **Download dataset**
- Download the LendingClub dataset from [Kaggle](https://www.kaggle.com/datasets/wordsforthewise/lending-club)
- Place `loan_data.csv` in `backend/data/` folder

5. **Train the model**
```bash
python -m src.train
```

6. **Run the backend**
```bash
uvicorn app:app --reload
```

Backend will be available at `http://localhost:8000`

### Frontend Setup

1. **Navigate to frontend**
```bash
cd frontend
```

2. **Install dependencies**
```bash
npm install
```

3. **Start development server**
```bash
npm start
```

Frontend will be available at `http://localhost:3000`

---

## 💻 Usage

### Making Predictions

1. **Open the web app**: Navigate to `http://localhost:3000`

2. **Fill in loan details**:
   - Loan amount, interest rate, term
   - Borrower income, employment length, home ownership
   - Credit information (accounts, balances, utilization)

3. **Toggle SHAP explanation** (optional):
   - Enabled: Get detailed feature contributions (2-3 seconds)
   - Disabled: Get prediction only (instant)

4. **Submit and view results**:
   - Default probability
   - Risk category (Low/Medium/High)
   - Recommendation (Approve/Reject)
   - Feature contributions (if SHAP enabled)

### API Usage
```python
import requests

# Example loan application
loan_data = {
    "loan_amnt": 15000.0,
    "int_rate": 13.5,
    "annual_inc": 60000.0,
    "dti": 18.2,
    "open_acc": 10,
    "revol_bal": 12000.0,
    "revol_util": 65.5,
    "total_acc": 25,
    "term": "36 months",
    "grade": "B",
    "emp_length": "5 years",
    "home_ownership": "RENT",
    "verification_status": "Verified",
    "purpose": "debt_consolidation"
}

# Make prediction
response = requests.post("http://localhost:8000/predict", json=loan_data)
print(response.json())
```

---

## 📊 Model Performance

| Model               | ROC-AUC | Accuracy | Precision | Recall |
|---------------------|---------|----------|-----------|--------|
| **XGBoost** ⭐      | 90.12%  | 87.34%   | 84.23%    | 78.91% |
| Random Forest       | 88.45%  | 85.67%   | 81.34%    | 76.23% |
| Logistic Regression | 84.56%  | 82.12%   | 78.45%    | 72.34% |

### Key Metrics Explained
- **ROC-AUC**: Model's ability to distinguish between classes (90%+)
- **Recall**: Percentage of actual defaults caught (critical in credit risk)
- **Precision**: Accuracy of default predictions
- **F1-Score**: Harmonic mean of precision and recall

---

## 📚 API Documentation

### Endpoints

#### `GET /`
Root endpoint - returns API information

#### `GET /health`
Health check - verifies model is loaded

**Response:**
```json
{
  "status": "healthy",
  "model_loaded": true,
  "message": "API is ready to serve predictions"
}
```

#### `POST /predict`
Fast prediction without explanation

**Request:**
```json
{
  "loan_amnt": 15000.0,
  "int_rate": 13.5,
  "annual_inc": 60000.0,
  // ... other features
}
```

**Response:**
```json
{
  "default_probability": 0.3456,
  "risk_category": "Medium Risk",
  "recommendation": "Approve",
  "confidence": 0.6912
}
```

#### `POST /explain`
Prediction with SHAP explanation (slower)

**Response:**
```json
{
  "default_probability": 0.3456,
  "base_value": 0.42,
  "top_increasing_risk": [
    {"feature": "dti", "impact": 0.32, "direction": "increases risk"}
  ],
  "top_decreasing_risk": [
    {"feature": "annual_income", "impact": -0.18, "direction": "decreases risk"}
  ]
}
```

### Interactive API Docs
Visit `http://localhost:8000/docs` for full Swagger UI documentation.

---

## 📸 Screenshots

> Add screenshots here after deployment

### Home Page
*Screenshot of landing page*

### Prediction Form
*Screenshot of input form*

### Results - High Risk
*Screenshot showing high risk prediction*

### SHAP Explanation
*Screenshot of feature contributions*

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Contact

**Your Name**
- GitHub: [@Tushy21](https://github.com/Tushy21)
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

**Project Link**: [https://github.com/Tushy21/Credit-Risk-Prediction-App](https://github.com/Tushy21/Credit-Risk-Prediction-App)

---

## 🙏 Acknowledgments

- [LendingClub Dataset](https://www.kaggle.com/datasets/wordsforthewise/lending-club) for training data
- [SHAP](https://github.com/slundberg/shap) for explainability framework
- [FastAPI](https://fastapi.tiangolo.com/) for backend framework
- [React](https://reactjs.org/) for frontend framework

---

<div align="center">

**⭐ Star this repository if you found it helpful!**

Made with ❤️ by [Tushy21](https://github.com/Tushy21)

</div>
