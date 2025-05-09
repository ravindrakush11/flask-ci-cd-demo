Here’s a **very basic Flask application** with **CI/CD pipelines** configured for **GitHub Actions**.

---

## 📦 Project Structure

```
flask-ci-cd-demo/
├── app.py
├── requirements.txt
├── test_app.py
├── .github/
│   └── workflows/
│       └── ci.yml
└── .gitlab-ci.yml
```

---

## 🐍 `app.py` – Basic Flask App

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello, CI/CD!'

if __name__ == '__main__':
    app.run()
```

---

## 📦 `requirements.txt`

```
Flask==3.1.0
pytest==8.3.3
gunicorn
```

---

## 🧪 `test_app.py` – Simple Test

```python
from app import app

def test_home():
    client = app.test_client()
    response = client.get('/')
    assert response.data == b'Hello, CI/CD!'
```

---

## ✅ GitHub Actions CI/CD – `.github/workflows/ci.yml`

```yaml
name: Flask CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'

    - name: Install dependencies
      run: |
        pip install -r requirements.txt

    - name: Run tests
      run: |
        pytest
```

---

## ✅ GitLab CI/CD – `.gitlab-ci.yml`

```yaml
stages:
  - test

test:
  image: python:3.10
  stage: test
  script:
    - pip install -r requirements.txt
    - pytest
```

---

## 💡 How to Run It

### For GitHub:

1. Push this project to a GitHub repository.
2. GitHub Actions will auto-trigger on push to `main`.

---

## 🚀 Use GitHub Actions Pipeline

### ✅ Step-by-Step:

#### 1. **Create a GitHub Repository**

* Go to [https://github.com/new](https://github.com/new)
* Name it something like `flask-ci-cd-demo`
* Make it public or private

#### 2. **Push the Project to GitHub**

If you already have the files locally (`app.py`, etc.), do:

```bash
git init
git remote add origin https://github.com/YOUR_USERNAME/flask-ci-cd-demo.git
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
```

#### 3. **CI/CD Happens Automatically**

Because you have the file `.github/workflows/ci.yml`, GitHub Actions will:

* Install Python
* Install your requirements
* Run your `pytest` tests

👉 **Check it**:

* Go to your repo on GitHub
* Click **Actions** tab
* You’ll see a workflow running ✅

---
