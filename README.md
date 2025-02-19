# Docker ML Model

We are going to create the ML model using Docker and train it accordingly.

## 📖 Documentation
- [Docker](https://www.docker.com/)
- [ML Model using Docker](https://mlmodel.com)
- [Machine Learning](https://machinelearning.com)

## 🛠️ Installation of ML Model and Docker

First, we will check if Docker and Python are installed in the system.

### For Docker:
```
docker --version
```

### For Python:
```
python --version
```

Now, we will import the ML model (already in GitHub):
```
app.py
```

## 📂 Project Structure
```
Docker-ML-model/
│── app/
│   ├── model.pkl          # Trained ML model
│   ├── main.py            # Backend script (FastAPI/Flask)
│   ├── requirements.txt   # Python dependencies
│── Dockerfile             # Docker build instructions
│── README.md              # Project documentation
│── .gitignore             # Ignore unnecessary files
```

## 🚀 Setup & Usage

### 1️⃣ Clone the Repository
```
git clone https://github.com/arryg5/Docker-ML-model.git
cd Docker-ML-model
```

### 2️⃣ Build the Docker Image
```
docker build -t docker-ml-model .
```

### 3️⃣ Run the Container
```
docker run -p 5000:5000 docker-ml-model
```

This will start the server, and you can access it at: `http://localhost:5000`

## 📡 API Endpoints
| Method | Endpoint | Description |
|--------|---------|-------------|
| POST | `/predict` | Send data to get predictions |

Example Request (Using cURL):
```
curl -X POST http://localhost:5000/predict -H "Content-Type: application/json" -d '{"feature": value}'
```

## 🐳 Useful Docker Commands

### Check running containers:
```
docker ps
```

### Stop a container:
```
docker stop <container_id>
```

### Remove a container:
```
docker rm <container_id>
```

### Remove an image:
```
docker rmi docker-ml-model
```

## 📦 Dockerfile
```
FROM python:3.8
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app/main.py"]
```

## 📝 main.py (FastAPI Example)
```
from fastapi import FastAPI
import pickle

app = FastAPI()

with open("app/model.pkl", "rb") as model_file:
    model = pickle.load(model_file)

@app.post("/predict")
def predict(data: dict):
    prediction = model.predict([data["features"]])
    return {"prediction": prediction.tolist()}

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=5000)
```

## 📌 Contributing
Feel free to contribute by submitting a PR or opening an issue! 🚀

## 📜 License
This project is licensed under the MIT License.

---
💡 *Maintained by [Aryaan Ghosal](https://github.com/arryg5)*


