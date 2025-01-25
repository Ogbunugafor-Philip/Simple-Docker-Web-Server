# Simple-Docker-Web-Server

## Introduction
The Simple Docker Web Server project is designed to showcase how Docker can be used quickly and easily deploy a basic web server. This project leverages Python's built-in HTTP server to serve static content, demonstrating how Docker containers can encapsulate an application with all its dependencies and configurations.

By following a few simple steps, you can build and run a Docker container that serves a custom `index.html` file, making it a perfect introduction to containerization and web deployment. Whether you're new to Docker or looking for a lightweight project to test your setup, this project offers a clear, practical example of how to containerize a web application and serve content over the web.

## Project Objectives
- Create a Dockerfile to define the web server environment.
- Build and run a Docker container.
- Serve static web pages via a Python-based HTTP server.
- Optionally, deploy the container to a cloud instance.

## Concept of Docker
Docker is a tool that enables developers to package applications and their dependencies into containers, ensuring that the application runs consistently across various environments, such as development, testing, and production.

For example:
- **In a development environment**, a developer might containerize a Python application on their local machine, including all required libraries like Flask or NumPy, to avoid dependency conflicts.
- **In a testing environment**, the same container can be deployed in a staging server or CI/CD pipeline, ensuring the application behaves identically to the development setup.
- **Finally, in a production environment**, the container can be deployed on cloud platforms (e.g., AWS, Google Cloud) or on-premises servers, guaranteeing consistent performance and reliability regardless of the hosting infrastructure.

By standardizing environments, Docker eliminates issues like "it works on my machine," providing a seamless application lifecycle from development to deployment.

## Key Components of Docker: Images, Containers and Dockerfile

### Dockerfile
A `Dockerfile` is a text file containing a series of instructions to build a Docker image.
- **Key Features**:
  - Declarative: Specifies how the image should be built, including the base image, application code, dependencies, and configurations.
  - Flexible: Can include commands to copy files, set environment variables, and run scripts.
- **Use Case**: Used to automate and version-control the creation of Docker images.

### Docker Images
A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software. This includes the code, runtime, libraries, environment variables, and configuration files.
- **Key Features**:
  - Immutable: Once built, they cannot be changed.
  - Layered: Built in layers, with each layer representing a set of instructions from the Dockerfile.
  - Portable: Can run on any system with Docker installed, ensuring consistency.
- **Use Case**: Serves as a blueprint for creating containers.

### Docker Containers
A container is a running instance of a Docker image. It is isolated and runs its processes independently of other containers and the host system.
- **Key Features**:
  - Lightweight: Shares the host OS kernel, making it more efficient than virtual machines.
  - Ephemeral: Can be started, stopped, and destroyed without affecting the image.
  - Isolated: Each container operates in its own environment.
- **Use Case**: Containers are used to run applications, ensuring they work the same in development, testing, and production environments.

## Dockerfile, Image and Container Building
We would do this hierarchically. First, we would create a Dockerfile, then build the Docker image using that file, and finally, run the image as a container.

We would do this using an AWS Ubuntu EC2 instance.

### Step 1: Docker Installation
1. Set up an EC2 instance and SSH into it:
   ```bash
   ssh -i "docker.pem" ubuntu@ec2-44-220-141-89.compute-1.amazonaws.com
   ```
2. Update the instance packages:
   ```bash
   sudo apt-get update
   ```
3. Install Docker:
   ```bash
   sudo apt-get install docker.io
   ```
4. Verify Docker Installation:
   ```bash
   docker --version
   ```
5. Start and Enable Docker:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

### Step 2: Create a Dockerfile, Build Image, and Run Container
1. Create a new folder and name it `simple-docker-server`:
   ```bash
   mkdir simple-docker-server
   ```
2. Change directory into the folder:
   ```bash
   cd simple-docker-server
   ```
3. In the directory, create 2 files: `Dockerfile` and `index.html`:
   ```bash
   touch Dockerfile
   touch index.html
   ```
4. Paste the following script in the `Dockerfile`:
   ```Dockerfile
   # Use the official Python image
   FROM python:3.9

   # Set the working directory
   WORKDIR /app

   # Copy all files into the container
   COPY . .

   # Expose port 8000
   EXPOSE 8000

   # Run Python's built-in HTTP server
   CMD ["python", "-m", "http.server", "8000"]
   ```
5. Paste the following script in the `index.html`:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Simple Docker Test</title>
   </head>
   <body>
       <h1>Hello, Docker World!</h1>
       <p>This is a test page served by a Docker container.</p>
   </body>
   </html>
   ```
6. To build the Docker image, run:
   ```bash
   docker build -t simple-html-server .
   ```
7. Run the Docker container:
   ```bash
   docker run -p 8000:8000 simple-html-server
   ```
8. Test your application by visiting `http://<your-instance-public-ip>:8000` in your browser.

## Conclusion
The Simple Docker Web Server project has successfully demonstrated how to leverage Docker to quickly set up and deploy a basic web server. By using Python's built-in HTTP server, we were able to serve static content in a containerized environment, showcasing the ease of managing applications with Docker.

This project serves as a fundamental introduction to containerization, illustrating how Docker simplifies application deployment by encapsulating the environment and dependencies. The ability to build, run, and serve content from a Docker container ensures that the application is portable, scalable, and isolated from the underlying system.

With this project, you've gained hands-on experience with Docker’s core concepts such as building images, creating Dockerfiles, and running containers. You can now apply this knowledge to more complex applications, expand your Docker skills, and explore further deployment options, including cloud environments.

This project lays the groundwork for building more advanced containerized applications and is a great starting point for anyone looking to dive deeper into Docker and containerization technology.
