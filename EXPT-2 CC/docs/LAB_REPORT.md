# Dockerized Python Flask Application

## 1. Aim

To package a simple Python Flask web application into a Docker image and run it locally in a Docker container using Docker Desktop.

## 2. Objectives

- Verify Docker installation and run the Docker `hello-world` test image.
- Create a Flask application and record its dependency.
- Build a Docker image from a Dockerfile.
- Run the application container with a host-to-container port mapping.
- Verify the image, container, and application response.

## 3. Requirements

- Windows computer with Docker Desktop installed and running
- Windows PowerShell
- Python application source and Dockerfile
- Web browser for testing `http://localhost:5000`

## 4. Software Used

| Software / Technology | Use |
|---|---|
| Windows | Operating system |
| PowerShell | Terminal used for commands |
| Docker Desktop | Local Docker environment |
| Docker | Image build and container lifecycle commands |
| Python 3.12 slim image | Container base image |
| Flask | Python web framework |
| Web browser | Accessing the local application |

## 5. Project Structure

```text
dockerized-python-flask-app/
├── app.py
├── requirements.txt
├── Dockerfile
├── README.md
├── .gitignore
├── LICENSE
└── docs/
    ├── LAB_REPORT.md
    └── screenshots/
        └── 01-12 experiment screenshots
```

## 6. Implementation

The application defines a Flask route at `/`. When requested, it returns `Hello! My first Docker application is running.` The server listens on `0.0.0.0:5000`, making it accessible through the container's published port. `requirements.txt` contains the `flask` package.

The project used in the experiment was located at `C:\Users\Asus\OneDrive\Desktop\docker-python-app`.

## 7. Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

The Dockerfile selects the Python base image, sets `/app` as the working directory, copies the dependency list and app, installs Flask, documents port 5000, and starts the Flask program when the container runs.

## 8. Commands Executed

Commands reported as used during the experiment:

```powershell
docker --version
docker run hello-world

cd "$HOME\OneDrive\Desktop"
mkdir docker-python-app
cd docker-python-app
pwd
dir

docker build -t my-python-app .
docker images
docker run -d -p 5000:5000 --name my-python-container my-python-app
docker ps
docker ps -a
docker start my-python-container
```

The container creation command encountered an existing-name conflict. The existing container was started and then verified. The browser test used `http://localhost:5000`.

## 9. Screenshots / Evidence

The submitted screenshots are included in [`screenshots/`](screenshots/). The README contains the numbered evidence table and embeds each image.

## 10. Output

The browser displayed:

> Hello! My first Docker application is running.

The running container was identified as `my-python-container`, with port mapping `0.0.0.0:5000->5000/tcp`.

## 11. Troubleshooting

- **Desktop path:** The Desktop directory was under OneDrive, so the experiment navigated with `cd "$HOME\OneDrive\Desktop"` rather than the assumed `C:\Users\Asus\Desktop` path.
- **Container name already in use:** An existing `my-python-container` was present. It was checked with `docker ps -a` and started with `docker start my-python-container`. A duplicate container was not created.

## 12. Learning Outcomes

The experiment demonstrated how a Dockerfile is used to build an image, how a container is run from that image, and how port publishing makes the Flask service available to a browser on the host. It also demonstrated the difference between an image and a container, and the use of `docker ps` and `docker ps -a` to check container state. Flask listened on `0.0.0.0` inside the container so that the published host port could reach it.

## 13. Conclusion

The Flask application was successfully built into a Docker image and run locally in a container. Port 5000 was mapped to the host, and the expected response was accessed through `localhost` in a browser.

## 14. Future Scope

These are possible extensions and were not performed as part of this lab: Docker Compose, Docker Hub publishing, CI/CD, Kubernetes, cloud deployment, container health checks, and a production WSGI server.
