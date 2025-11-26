# DevOps-Project

Simple static app served in Docker.

## Project Structure

- `Dockerfile` - builds the image
- `app/` - web content
  - `index.html`

## Prerequisites

- Docker installed and running

## Build

From the project root run:

```powershell
docker build -t priyanka4316/devops-app:v1 .
```

## Run

To start the container and map port 8080 on your host to port 80 in the container:

```powershell
docker run -d -p 8080:80 priyanka4316/devops-app:v1
```

Then open http://localhost:8080 in your browser.

## Notes

- To change the web content edit `app/index.html` and rebuild the image.
- Tag/version as needed (e.g., `v1`, `v1.1`).

---

