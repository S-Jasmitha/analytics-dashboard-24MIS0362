# Analytics Dashboard — 24MIS0362

## Features
- V1: Add data
- V2: View data
- V3: Chart

## 1. Run without Docker first
Open this folder in VS Code. You can open each `v1/index.html`, `v2/index.html`, or `v3/index.html` in a browser, or use VS Code Live Server.

## 2. Docker (if installed)
From the project root, run:
```bash
docker --version
docker build -t YOUR_DOCKERHUB_USERNAME/analytics-dashboard:v1 ./v1
docker build -t YOUR_DOCKERHUB_USERNAME/analytics-dashboard:v2 ./v2
docker build -t YOUR_DOCKERHUB_USERNAME/analytics-dashboard:v3 ./v3
docker run -d --name analytics-v1 -p 8081:80 YOUR_DOCKERHUB_USERNAME/analytics-dashboard:v1
docker run -d --name analytics-v2 -p 8082:80 YOUR_DOCKERHUB_USERNAME/analytics-dashboard:v2
docker run -d --name analytics-v3 -p 8083:80 YOUR_DOCKERHUB_USERNAME/analytics-dashboard:v3
```
Open http://localhost:8081, http://localhost:8082, and http://localhost:8083.
Replace `YOUR_DOCKERHUB_USERNAME` with your Docker Hub username.

## 3. GitHub
Create an empty GitHub repository, then from this folder:
```bash
git init
git add .
git commit -m "v1: add analytics data input"
git branch v1
git add .
git commit -m "v2: add data viewing"
git branch v2
git add .
git commit -m "v3: add chart visualization"
git branch v3
git branch
git log --oneline
```
To connect and push, replace the URL:
```bash
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
git push origin v1 v2 v3
```
These are separate version branches, while the commits show the staged progression. For genuinely version-specific commits, commit each version's changes before moving to the next version.

## 4. Jenkins
- Install/start Jenkins and ensure Docker is available to the Jenkins agent.
- Add a Jenkins credential of type Username with password; ID: `dockerhub-creds`. Username = Docker Hub username, password = Docker Hub access token.
- Create a Pipeline job connected to your GitHub repository, or use “Pipeline script from SCM”.
- Keep the supplied `Jenkinsfile` at the repository root.
- Run Build Now and capture the successful stage/log evidence.
- The Jenkinsfile pushes the three images to Docker Hub when credentials and Docker access are correctly configured.

## 5. Kubernetes
Prerequisites: a working Kubernetes cluster (for example Docker Desktop Kubernetes) and `kubectl`.
Apply:
```bash
kubectl apply -f k8s/
kubectl get deployments
kubectl get services
```
Open:
- http://localhost:30081
- http://localhost:30082
- http://localhost:30083

If Docker Hub images are private, make them public for this demo or configure an imagePullSecret. If Kubernetes is not available, do not claim deployment succeeded; take screenshots of the manifest and note the prerequisite.

## Screenshots checklist
1. V1 page showing the input form.
2. V2 page showing the saved-data list.
3. V3 page showing the chart.
4. GitHub repository and `git log --oneline`.
5. Docker images (`docker images`) with v1/v2/v3 tags.
6. Docker containers (`docker ps`) and the three localhost pages.
7. Docker Hub repository tags v1/v2/v3.
8. Jenkins successful pipeline stages.
9. `kubectl get deployments` and `kubectl get services`.
10. Kubernetes pages on localhost ports 30081–30083.

## Handwritten procedure
Write the following in your record in your own handwriting, and only mark steps as completed when you have actually done them:

1. Created the Analytics Dashboard project in VS Code.
2. Developed V1 to enter analytics values.
3. Developed V2 to display the entered values.
4. Developed V3 to visualize values using a chart.
5. Initialized Git and committed the versions; created version branches and pushed the project to GitHub.
6. Created Docker images and tagged them v1, v2, and v3.
7. Configured a Jenkins pipeline to build the project/images.
8. Pushed the Docker images to Docker Hub.
9. Created three Kubernetes Deployments and Services.
10. Exposed the services on separate local ports and tested each version.
11. Captured screenshots of the application, GitHub, Docker, Jenkins, Docker Hub, and Kubernetes outputs.

Note: Steps 6–10 depend on Docker, Jenkins, Docker Hub access, and a working Kubernetes cluster.
