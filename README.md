# Heart Disease Prediction Deployment

An end-to-end machine learning project that predicts whether a patient is at risk of heart disease based on clinical parameters. The model is trained on the Heart Disease Prediction dataset, served via a Flask REST API, and deployed live on Render.

## Live Demo
**Deployed API:** https://heart-disease-deployment-cmbj.onrender.com

## Dataset
- **Source:** [Heart Disease Prediction Dataset (Kaggle)](https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset)
- **Total records:** 1025
- **Target variable:** `target` (1 = heart disease present, 0 = no heart disease)
- **Numerical/clinical features:** age, sex, cp, trestbps, chol, fbs, restecg, thalach, exang, oldpeak, slope, ca, thal
- **Missing values:** None (verified during preprocessing)

## Model
- **Algorithm used:** Random Forest Classifier (n_estimators=200, random_state=42)
- **Train/test split:** 80% / 20% (820 training samples, 205 testing samples)
- **Accuracy achieved:** 98.54%
- **Model file:** `model.pkl` (saved using joblib)

## Project Structure
```
HeartDiseaseDeployment/
│
├── app.py                # Flask application
├── model.pkl              # Trained model
├── requirements.txt        # Python dependencies
├── runtime.txt              # Python version pin for Render
├── README.md
├── train_model.py          # Model training script
├── heart.csv               # Dataset
└── templates/
    └── index.html 
```

## Tech Stack
- Python 3.11.9
- Flask (REST API)
- scikit-learn (model training)
- pandas, numpy (data processing)
- Gunicorn (production WSGI server)
- Render (cloud deployment)

## API Usage

### Endpoint
```
POST /predict
```

### Example Request
```json
{
  "age": 63,
  "sex": 1,
  "cp": 3,
  "trestbps": 145,
  "chol": 233,
  "fbs": 1,
  "restecg": 0,
  "thalach": 150,
  "exang": 0,
  "oldpeak": 2.3,
  "slope": 0,
  "ca": 0,
  "thal": 1
}
```

### Example Response
```json
{
  "prediction": "Heart Disease Detected"
}
```

### Test it yourself (Windows CMD)
```
curl -X POST https://heart-disease-deployment-cmbj.onrender.com/predict -H "Content-Type: application/json" -d "{\"age\":63,\"sex\":1,\"cp\":3,\"trestbps\":145,\"chol\":233,\"fbs\":1,\"restecg\":0,\"thalach\":150,\"exang\":0,\"oldpeak\":2.3,\"slope\":0,\"ca\":0,\"thal\":1}"
```

## Running Locally
```bash
git clone https://github.com/Sparvathy-23/Heart-Disease-Deployment.git
cd Heart-Disease-Deployment
pip install -r requirements.txt
python app.py
```

## Conclusion
The Random Forest Classifier trained on the Heart Disease Prediction dataset achieved an accuracy of 98.54% on the test set, demonstrating strong performance in distinguishing patients at risk of heart disease based on clinical parameters such as age, cholesterol, and chest pain type.

During deployment, the main challenge faced was a Python version compatibility issue on Render. The platform defaulted to Python 3.14, which caused pandas to fail during installation due to unresolved build errors in its C++ extensions. This was resolved by explicitly pinning the Python version to 3.11.9 using an environment variable, which allowed all dependencies to install correctly from precompiled wheels rather than being built from source.

This project highlighted the importance of MLOps practices in real-world machine learning systems. Beyond building an accurate model, successfully packaging it, managing dependencies, version-controlling the codebase, and deploying it as a reliable, publicly accessible API are essential steps that ensure a model can move from experimentation to production. Practices like environment reproducibility and automated deployment pipelines are critical for maintaining stability and scalability in real-world ML applications.

## Author
- **Name:** Sree Parvathy P Nair
