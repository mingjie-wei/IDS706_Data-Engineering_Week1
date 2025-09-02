# IDS706_Data-Engineering_Week1
[![Python Template for IDS706](https://github.com/mingjie-wei/IDS706_Data-Engineering_Week1/actions/workflows/main.yml/badge.svg)](https://github.com/mingjie-wei/IDS706_Data-Engineering_Week1/actions/workflows/main.yml)


## Approach: Local Setup Workflow

### Clone the project in Terminal
```bash
cd ~/Desktop
git clone https://github.com/mingjie-wei/IDS706_Data-Engineering_Week1.git
```

### Open the project with VS Code
```bash
cd IDS706_Data-Engineering_Week1  # Enter the folder I just cloned
code .                            # Open the current directory with VS Code
```

### Create new files in the repository
```bash
touch Makefile
touch hello.py
touch test_hello.py
touch requirements.txt
```

### Setup Python Environment (if you're not using a Dev Container)
If you're working outside of a dev container, you can manually create and activate a virtual environment. If you do so, for consistency, it's recommended to name the environment the same as your repository.

```bash
python3 -m venv ~/.IDS706_Data-Engineering_Week1
source ~/.IDS706_Data-Engineering_Week1/bin/activate
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

### VS Code Dev Containers (Suggested)
Open a sample in a container by pressing shift+command+P, then select `Dev Containers: Add Development Container Configuration Files...`. Choose the Python 3.11 template, and it will create the necessary files for you.

#### Rebuild or update your container
after you make changes to your container, such as installing a packages, you'll rebuild your container for your changes to take effect. by pressing shift+command+P, then select `Dev Containers: Rebuild Container` or `Codespaces: Rebuild Container` command so the modifications are picked up.  

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

### Commit and push your changes via commands or User Interface
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
