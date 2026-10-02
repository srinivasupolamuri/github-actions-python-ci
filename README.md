# Python CI Pipeline with GitHub Actions

![GitHub
Actions](https://img.shields.io/badge/GitHub%20Actions-CI-blue?logo=githubactions)
![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python)
![Pytest](https://img.shields.io/badge/Tests-Pytest-green?logo=pytest)

## 📌 Project Overview

This project demonstrates a basic **Continuous Integration (CI) pipeline
using GitHub Actions**.

A simple Python calculator application is used as the sample
application. Whenever code is pushed to the `main` branch or a pull
request is opened against `main`, GitHub Actions automatically:

1.  Checks out the source code.
2.  Sets up the required Python environment.
3.  Installs project dependencies.
4.  Executes automated tests using Pytest.
5.  Reports the pipeline result as Success or Failure.

The project was built as a practical introduction to GitHub Actions and
CI automation.

------------------------------------------------------------------------

## 🎯 Project Objectives

-   Understand the fundamentals of GitHub Actions.
-   Create a workflow using a YAML configuration file.
-   Understand workflows, jobs, steps, triggers, and runners.
-   Automate Python application testing.
-   Implement automated testing on every push to `main`.
-   Implement CI validation for pull requests targeting `main`.
-   Understand the difference between local testing and GitHub-hosted CI
    execution.

------------------------------------------------------------------------

## 🏗️ Project Architecture

``` text
Developer / Local Ubuntu
        |
        | git push
        v
GitHub Repository
        |
        | Push / Pull Request
        v
GitHub Actions
        |
        v
Ubuntu GitHub-Hosted Runner
        |
        +--------------------------+
        |                          |
        v                          v
Checkout Source Code        Setup Python 3.13
        |                          |
        +------------+-------------+
                     |
                     v
             Install Dependencies
                     |
                     v
                Run Pytest
                     |
             +-------+-------+
             |               |
             v               v
          PASS ✓           FAIL ✗
```

------------------------------------------------------------------------

## 🛠️ Technologies Used

  Technology       Purpose
  ---------------- ---------------------------------------------
  Git              Source code version control
  GitHub           Source code repository
  GitHub Actions   CI workflow automation
  YAML             Workflow configuration
  Python 3.13      Application runtime
  Pytest           Automated testing
  Ubuntu           Local development and GitHub Actions runner
  VS Code          Development environment
  WSL              Local Linux development environment

------------------------------------------------------------------------

## 📁 Project Structure

``` text
github-actions-python-ci/
│
├── .github/
│   └── workflows/
│       └── python-ci.yml
│
├── src/
│   └── calculator.py
│
├── tests/
│   └── test_calculator.py
│
├── .gitignore
├── README.md
└── requirements.txt
```

### Directory and File Description

#### `.github/workflows/python-ci.yml`

Contains the GitHub Actions workflow definition.

#### `src/calculator.py`

Contains the Python calculator functions:

-   Addition
-   Subtraction
-   Multiplication
-   Division

#### `tests/test_calculator.py`

Contains automated Pytest test cases for the calculator functions.

#### `requirements.txt`

Contains the Python dependency required by the project:

``` text
pytest
```

#### `.gitignore`

Prevents unnecessary local files such as virtual environments, Python
cache files, and Pytest cache from being committed.

------------------------------------------------------------------------

## ⚙️ GitHub Actions Workflow

The workflow is stored at:

``` text
.github/workflows/python-ci.yml
```

Current workflow:

``` yaml
name: Python CI Pipeline

on:
  push:
    branches:
      - main

  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@v7

      - name: Set up Python
        uses: actions/setup-python@v7
        with:
          python-version: '3.13'
          cache: 'pip'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run tests
        run: |
          pytest -v
```

------------------------------------------------------------------------

## 🔍 Workflow Explanation

### 1. Workflow Name

``` yaml
name: Python CI Pipeline
```

Defines the name displayed in the GitHub Actions interface.

### 2. Workflow Triggers

``` yaml
on:
  push:
    branches:
      - main
```

The workflow automatically runs when code is pushed to the `main`
branch.

It also runs for pull requests targeting `main`:

``` yaml
pull_request:
  branches:
    - main
```

### 3. Job

``` yaml
jobs:
  test:
```

Defines a job named `test`.

### 4. Runner

``` yaml
runs-on: ubuntu-latest
```

The job runs on a GitHub-hosted Ubuntu runner.

No AWS EC2 instance is required for this project.

### 5. Checkout Source Code

``` yaml
uses: actions/checkout@v7
```

Checks out the repository source code so that subsequent workflow steps
can access the project files.

### 6. Set Up Python

``` yaml
uses: actions/setup-python@v7
```

Configures Python 3.13 for the CI environment.

Pip caching is enabled to improve dependency installation performance.

### 7. Install Dependencies

``` yaml
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Upgrades pip and installs the dependencies listed in `requirements.txt`.

### 8. Run Automated Tests

``` yaml
pytest -v
```

Executes the project's automated test cases and displays detailed test
results.

------------------------------------------------------------------------

## 🧪 Application Testing

The project contains four automated test cases:

``` text
test_add
test_subtract
test_multiply
test_divide
```

Expected result:

``` text
4 passed
```

A successful workflow indicates that all configured tests have passed.

------------------------------------------------------------------------

## 💻 Run the Project Locally

### Prerequisites

Install:

-   Python 3
-   Git
-   Pytest
-   Ubuntu/WSL or another Linux environment

### 1. Clone the Repository

``` bash
git clone https://github.com/<your-username>/github-actions-python-ci.git
cd github-actions-python-ci
```

### 2. Create a Virtual Environment

``` bash
python3 -m venv venv
```

### 3. Activate the Virtual Environment

``` bash
source venv/bin/activate
```

### 4. Install Dependencies

``` bash
pip install -r requirements.txt
```

### 5. Run Tests

``` bash
pytest -v
```

Expected result:

``` text
tests/test_calculator.py::test_add PASSED
tests/test_calculator.py::test_subtract PASSED
tests/test_calculator.py::test_multiply PASSED
tests/test_calculator.py::test_divide PASSED

4 passed
```

------------------------------------------------------------------------

## 🚀 Git Workflow

The project follows a simple development workflow:

``` text
Create / Modify Code
        |
        v
Run Tests Locally
        |
        v
git add .
        |
        v
git commit
        |
        v
git push origin main
        |
        v
GitHub Actions
        |
        v
Automated Tests
```

Example:

``` bash
git add .
git commit -m "Update calculator tests"
git push origin main
```

After the push, GitHub Actions automatically starts the CI workflow.

------------------------------------------------------------------------

## ✅ CI Validation

After pushing code to GitHub:

1.  Open the repository.
2.  Select the **Actions** tab.
3.  Select **Python CI Pipeline**.
4.  Open the workflow run.
5.  Select the `test` job.
6.  Review each workflow step and the Pytest output.

A successful execution appears with a green check mark.

------------------------------------------------------------------------

## 🔐 Security Considerations

No passwords, Personal Access Tokens, AWS credentials, or other
sensitive credentials are stored in the repository.

GitHub authentication used for Git operations is handled outside the
source code.

Sensitive credentials should never be hard-coded into:

-   Python source files
-   YAML workflow files
-   README files
-   Git commits

For future deployment projects, secrets should be managed using GitHub
Actions Secrets/Variables or appropriate cloud identity mechanisms.

------------------------------------------------------------------------

## 🧩 Troubleshooting

### Workflow does not start

Check that the workflow file is located exactly at:

``` text
.github/workflows/python-ci.yml
```

Also verify that the push is being made to:

``` text
main
```

### Pytest command not found

Install the project dependencies:

``` bash
pip install -r requirements.txt
```

### Tests fail locally

Run:

``` bash
pytest -v
```

Review the failed test and correct the application or test code before
pushing.

### GitHub Actions fails during dependency installation

Check:

``` text
requirements.txt
```

and verify that all required packages are listed correctly.

------------------------------------------------------------------------

## 📚 Key GitHub Actions Concepts Learned

This project demonstrates the following concepts:

-   GitHub Actions
-   Workflow
-   YAML
-   Workflow triggers
-   `push` event
-   `pull_request` event
-   Jobs
-   Steps
-   GitHub-hosted runners
-   `runs-on`
-   Actions
-   `actions/checkout`
-   `actions/setup-python`
-   Dependency installation
-   Pip caching
-   Automated testing
-   Pytest
-   CI pipeline execution
-   Git and GitHub integration

------------------------------------------------------------------------

## 🎓 Interview Explanation

### What did you build?

> I created a Python CI pipeline using GitHub Actions. The workflow is
> triggered when code is pushed to the main branch or when a pull
> request targets the main branch. It checks out the source code,
> configures Python 3.13, installs the project dependencies, and
> executes automated tests using Pytest. The workflow runs on a
> GitHub-hosted Ubuntu runner and reports whether the tests passed or
> failed.

### Why did you use GitHub Actions?

> GitHub Actions is integrated with GitHub and allows CI/CD workflows to
> be automated directly from the repository. It removes the need to
> manually run validation after every code change.

### Do you need an EC2 instance?

> No. This project uses a GitHub-hosted Ubuntu runner for CI execution.
> An EC2 instance would only be required if the pipeline needed to
> deploy the application to an AWS server.

### What happens after a developer pushes code?

> GitHub detects the push event, triggers the workflow, starts a runner,
> checks out the source code, installs Python and dependencies, runs the
> automated tests, and reports the final result.

------------------------------------------------------------------------

## 🔮 Future Enhancements

This project is intentionally kept simple as a foundational CI project.

Possible future improvements include:

-   Test multiple Python versions using a matrix strategy.
-   Add code quality/linting checks.
-   Add code coverage reporting.
-   Build a Docker image.
-   Push the Docker image to Docker Hub or GitHub Container Registry.
-   Add deployment to AWS EC2.
-   Add Terraform infrastructure automation.
-   Add environment-specific deployments.
-   Add CI/CD approval and deployment stages.

------------------------------------------------------------------------

## 👨‍💻 Project Type

**DevOps / CI Automation / GitHub Actions**

This project was created as a hands-on learning project to understand
and implement Continuous Integration using GitHub Actions.
