# CI/CD Pipeline with Docker & GitHub Actions

A minimal Flask app with a full CI/CD pipeline: every push runs automated tests, builds a Docker image, and pushes it to Docker Hub using GitHub Actions.

## What this project demonstrates
- Containerizing an application with Docker
- Automated testing in CI
- Automated Docker build & push on merge to `main`
- GitHub Actions workflows (industry-standard CI/CD tool)

## Project structure
```
01-cicd-docker-github-actions/
├── app/
│   ├── app.py
│   └── requirements.txt
├── tests/
│   └── test_app.py
├── .github/workflows/ci-cd.yml
├── Dockerfile
└── README.md
```

## Steps to run locally

1. Install dependencies:
   ```bash
   cd app
   pip install -r requirements.txt
   ```
2. Run the app:
   ```bash
   python app.py
   ```
3. Visit `http://localhost:5000` and `http://localhost:5000/health`.

4. Run tests:
   ```bash
   pytest tests/ -v
   ```

## Steps to run with Docker

```bash
docker build -t cicd-demo-app .
docker run -p 5000:5000 cicd-demo-app
```

## Steps to upload to GitHub and activate the pipeline

1. Create a new repository on GitHub (e.g. `cicd-docker-github-actions`).
2. From this project folder:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: CI/CD pipeline with Docker + GitHub Actions"
   git branch -M main
   git remote add origin https://github.com/<your-username>/cicd-docker-github-actions.git
   git push -u origin main
   ```
3. Create a free [Docker Hub](https://hub.docker.com) account (if you don't have one).
4. In your GitHub repo: **Settings → Secrets and variables → Actions → New repository secret**, add:
   - `DOCKERHUB_USERNAME` = your Docker Hub username
   - `DOCKERHUB_TOKEN` = a Docker Hub access token (Docker Hub → Account Settings → Security → New Access Token)
5. Push a small change — go to the **Actions** tab on GitHub and watch the pipeline run automatically (test → build → push).

## What to put on your resume
> "Built and deployed a containerized Flask application with an automated CI/CD pipeline using GitHub Actions — automated testing, Docker image builds, and registry push on every commit."

## Possible extensions (if you have extra time later)
- Deploy the image automatically to AWS ECS / Render / Railway free tier.
- Add code coverage reporting and a status badge to the README.
- Add linting (flake8/black) as a pipeline stage.
