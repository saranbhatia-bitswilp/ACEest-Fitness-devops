# ACEest Fitness & Gym - DevOps CI/CD Project

## Overview

ACEest Fitness & Gym is a Flask-based application developed for the BITS Pilani Introduction to DevOps assignment.

The project demonstrates a complete DevOps workflow using Git/GitHub, Python Flask, Pytest, Docker, GitHub Actions, and Jenkins.

## Application Features

The Flask application provides these endpoints:

| Endpoint | Method | Description |
|---|---|---|
| `/` | GET | Application status and welcome message |
| `/health` | GET | Application health check |
| `/programs` | GET | Returns available fitness programs |
| `/calculate-calories` | POST | Calculates estimated calories using program and weight |

Available programs are Fat Loss, Muscle Gain, and Beginner.

## Project Structure

- `app.py` - Flask application
- `requirements.txt` - Python dependencies
- `test_app.py` - Pytest test suite
- `Dockerfile` - Docker image definition
- `.dockerignore` - Docker exclusions
- `.gitignore` - Git exclusions
- `.github/workflows/ci.yml` - GitHub Actions CI workflow
- `README.md` - Project documentation

## Local Setup

Clone the repository:

    git clone https://github.com/saranbhatia-bitswilp/ACEest-Fitness-devops.git
    cd ACEest-Fitness-devops

Create and activate a Python virtual environment:

    python3 -m venv .venv
    source .venv/bin/activate

Install dependencies:

    python -m pip install --upgrade pip
    python -m pip install -r requirements.txt

## Run the Application

Start the Flask application:

    python app.py

The service listens on:

    http://127.0.0.1:5000

Health check:

    curl http://127.0.0.1:5000/health

Expected response:

    {"status":"healthy"}

## Manual Testing

Run the Pytest suite:

    python -m pytest -v test_app.py

The project contains six automated tests covering:

1. Home endpoint
2. Health endpoint
3. Programs endpoint
4. Valid calorie calculation
5. Invalid program validation
6. Invalid weight validation

Verified result:

    6 passed

## Docker

Build the image:

    docker build -t aceest-fitness:local .

Run the application:

    docker run --rm -p 5000:5000 aceest-fitness:local

Run Pytest inside Docker:

    docker run --rm -v "$PWD:/app:ro" -w /app aceest-fitness:local python -m pytest -v -p no:cacheprovider test_app.py

Verified Dockerized test result:

    6 passed

## GitHub Actions

The workflow is stored in:

    .github/workflows/ci.yml

It is triggered on pushes to `main` and pull requests targeting `main`.

The workflow performs:

1. Source checkout
2. Python setup
3. Dependency installation
4. Python syntax validation
5. Pytest execution
6. Docker image build
7. Pytest execution inside Docker

The GitHub Actions workflow has been successfully validated.

## Jenkins Integration

A Jenkins Freestyle project named `ACEest-Fitness-BUILD` was configured to retrieve the latest source code from:

    https://github.com/saranbhatia-bitswilp/ACEest-Fitness-devops.git

The Jenkins BUILD performs:

1. Clean GitHub checkout
2. Python, Git, and Docker environment checks
3. Python syntax validation
4. Clean Docker image build
5. Pytest execution inside Docker
6. Docker image verification

Verified Jenkins result:

    6 passed
    JENKINS BUILD COMPLETED SUCCESSFULLY
    Finished: SUCCESS

## Verified Results

| Validation | Result |
|---|---|
| Python syntax validation | PASS |
| Local Pytest | 6/6 PASS |
| Docker image build | PASS |
| Docker application validation | PASS |
| Dockerized Pytest | 6/6 PASS |
| GitHub Actions | SUCCESS |
| Jenkins BUILD | SUCCESS |

## Repository

https://github.com/saranbhatia-bitswilp/ACEest-Fitness-devops

## Author

BITS Pilani Work Integrated Learning Programme

Student ID: **2026ht66039**
