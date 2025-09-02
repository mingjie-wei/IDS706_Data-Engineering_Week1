# IDS706_Data-Engineering_Week1
[![Python Template for IDS706](https://github.com/mingjie-wei/IDS706_Data-Engineering_Week1/actions/workflows/main.yml/badge.svg)](https://github.com/mingjie-wei/IDS706_Data-Engineering_Week1/actions/workflows/main.yml)

## First Approach: Cloud-based Containerized Setup Workflow (With Dev Container)

### Create new files in the repository
```bash
touch Makefile
touch hello.py
touch test_hello.py
touch requirements.txt
```

### Create a Makefile
```makefile
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

format:
	black *.py

lint:
	flake8 hello.py

test:
	python -m pytest -vv --cov=hello test_hello.py

clean:
    rm -rf __pycache__ .pytest_cache .coverage

all: install format lint test

```

### Create a requirements.txt file
```text
pylint
flake8
pytest
click
black
pytest-cov
```

### Run the Makefile
```bash 
make install
```

### Create a simple Python script
```python
def say_hello(name: str) -> str:
    """Return a greeting message to students in the IDS class."""
    return f"Hello, {name}, welcome to Data Engineering Systems (IDS 706)!"


def add(a: int, b: int) -> int:
    """Return the sum of two numbers."""
    return a + b
```

### Create a test file
```python
from hello import say_hello, add

def test_say_hello():
    assert (
        say_hello("Annie")
        == "Hello, Annie, welcome to Data Engineering Systems (IDS 706)!"
    )

def test_add():
    assert add(2, 3) == 5
```

### Run the tests
```bash 
make test
``` 

### Format the code
```bash 
make format
```

### Lint the code
```bash
make lint
```

### Clean up the environment
```bash
make clean
```

### Commit and push your changes via commands
```bash
git add .
git commit -m "Initial commit with Python template setup"   
git push origin main
``` 

### View your repository

### Enable GitHub Actions

1. Go to your repository on GitHub.
2. Click on the "Actions" tab.
3. Click on "New workflow".
4. Select "Set up a workflow yourself".
5. Replace the content with the following YAML configuration:

```yaml
name: Python Template for IDS706

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.11'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Lint with flake8
      run: flake8 hello.py
    - name: Run tests
      run: pytest --cov=hello

```
6. Commit and push this file to your repository.
7. GitHub Actions will run automatically on every push or pull request!

### View the Actions tab 

1. Go to the "Actions" tab in your repository.
2. You should see the workflow running.
3. Click on the latest workflow run to see the details.


## Second Approach: Local Setup Workflow