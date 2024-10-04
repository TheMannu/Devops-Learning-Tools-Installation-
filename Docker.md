Here’s a summary of the scripting approach for downloading, installing Docker, and managing containers:

### **1. Download and Install Docker**
```bash
sudo -i
curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh
```
- Use `curl` to download the Docker installation script.
- Run the script using `sh` to install Docker.

### **2. Verify Docker Installation**
```bash
docker pull hello-world
docker run hello-world
docker ps
docker ps -a
```
- `docker pull hello-world`: Downloads the image.
- `docker run hello-world`: Downloads and runs the image.
- `docker ps`: Shows running containers.
- `docker ps -a`: Shows all containers.

### **3. Docker Lifecycle Commands**
- **Start a container interactively**:
  ```bash
  docker run -it ubuntu
  exit
  ```
- **Manage Containers**:
  - `docker start <CONTAINER ID>`: Start a stopped container.
  - `docker logs <CONTAINER ID>`: View logs of a container.
  - `docker inspect <CONTAINER ID>`: Detailed container information.
  - `docker rm <CONTAINER ID>`: Remove a container.
  - `docker exec -it <CONTAINER ID> bin/bash`: Enter a running container.

### **4. Working with Nginx**
- **Basic Nginx container**:
  ```bash
  docker run -p 80:80 nginx
  ```
- **Run Nginx with a custom HTML**:
  ```bash
  mkdir -p ~/docker-nginx/html
  cd ~/docker-nginx/html
  vi index.html
  docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx
  ```

### **5. Dockerfile Example**
```dockerfile
FROM ubuntu
MAINTAINER clouddevopshub@gmail.com
RUN apt-get update
RUN apt-get install nginx -y
CMD ["echo", "Image created"]
```
- Build and push image:
  ```bash
  docker build -t mynginxbatch35 .
  docker login
  docker push <docker-hub-username>/mynginxbatch35
  ```

### **6. Backup and Restore Docker Image**
- **Commit a running container to an image**:
  ```bash
  docker commit <CONTAINER ID> <new image name>
  ```
- **Save and upload to S3**:
  ```bash
  docker save <image name> > mybackup.tar
  aws s3 cp mybackup.tar s3://<bucket-name>
  ```

### **7. Monitoring and Cleanup**
- **Monitor containers**:
  ```bash
  docker logs -f <container name>
  docker stats <container ID>
  docker top <container name>
  ```
- **Clean up unused images**:
  ```bash
  docker image prune -a
  ```

This script covers Docker installation, managing containers, building images, backups, and cleanup.
