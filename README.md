# Demo: Dockerize a Python Flask App

This is a **simple demo project** showing how to create a Docker container for a Python Flask application (`app.py`) and run it.

---

## **Project Structure**

```

docker_demo/
├── app.py          # Simple Flask application
├── Dockerfile      # Dockerfile to build the container
├── requirements.txt # Python dependencies
└── README.md       # This file

````

---

## **1️⃣ Flask Application (`app.py`)**

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
````

---

## **2️⃣ Dockerfile**

```dockerfile
# Use Python 3.11 slim image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Copy dependencies and install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy app code
COPY . .

# Expose port 5000
EXPOSE 5000

# Run Flask app
CMD ["python", "app.py"]
```

---

## **3️⃣ Python Dependencies (`requirements.txt`)**

```
flask
```

---

## **4️⃣ Build and Run the Docker Container**

1. **Build the image**:

```bash
docker build -t flask-demo .
```

2. **Run the container**:

```bash
docker run -p 5000:5000 flask-demo
```

3. **Access the app**:

Open your browser:

```
http://localhost:5000/
```

You should see:

```
Hello, Docker!
```

---

## **5️⃣ Optional: Run in Detached Mode**

```bash
docker run -d -p 5000:5000 flask-demo
```

* `-d` → runs the container in the background

---

## **6️⃣ Stop the Container**

1. List running containers:

```bash
docker ps
```

2. Stop the container:

```bash
docker stop <container_id>
```

---

## **Author**

