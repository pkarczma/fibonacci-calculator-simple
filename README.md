# React Frontend Application

A React frontend application built with Create React App, featuring Docker containerization and automated deployment to AWS Elastic Beanstalk.

## 🚀 Features

- **React 18** with modern hooks and functional components
- **Docker** containerization for both development and production
- **Automated CI/CD** pipeline with GitHub Actions
- **AWS Elastic Beanstalk** deployment
- **Multi-stage Docker builds** for optimized production images
- **Docker Compose** development environment

## 📋 Prerequisites

- **Docker** and Docker Compose
- **AWS account** (for deployment)

## 🛠️ Getting Started

### Quick Development Setup (Recommended)

Use Docker Compose to quickly spin up the entire development environment with a single command. This approach automatically handles all dependencies and provides both the web server and test runner.

1. **Start the development environment:**
   ```bash
   docker-compose -f docker-compose-dev.yml up
   ```

   This will start:
   - **Web server** on port 3000 with live reloading
   - **Test runner** in watch mode

2. **Access the application:**
   - Frontend: [http://localhost:3000](http://localhost:3000)
   - Tests run automatically in the background

3. **Stop the environment:**
   ```bash
   docker-compose -f docker-compose-dev.yml down
   ```

### Advanced Docker Usage

In order to have more control over the Docker build process or to understand the underlying containerization, use these manual Docker commands.

**Development Container:**
```bash
docker build -f Dockerfile.dev -t frontend-dev .
docker run -p 3000:3000 -v $(pwd):/app -v /app/node_modules frontend-dev
```

**Production Container:**
```bash
docker build -t frontend-prod .
docker run -p 80:80 frontend-prod
```

The production build uses a multi-stage approach:
1. **Build stage**: Uses Node.js to build the React app
2. **Runtime stage**: Uses Nginx to serve the static files

## 🚀 Deployment

### Automated Deployment (GitHub Actions)

The application automatically deploys to AWS Elastic Beanstalk when code is pushed to the `main` branch.

**Deployment Pipeline:**
1. **Build**: Creates Docker image using development Dockerfile
2. **Test**: Runs the test suite in CI environment
3. **Package**: Creates deployment package
4. **Deploy**: Deploys to AWS Elastic Beanstalk

**Required GitHub Secrets:**
- `DOCKER_USERNAME`: Docker Hub username
- `DOCKER_PASSWORD`: Docker Hub password  
- `AWS_ACCESS_KEY_ID`: AWS access key
- `AWS_SECRET_KEY`: AWS secret key

### Manual Deployment

1. **Build the production image:**
   ```bash
   docker build -t pkarczmarczyk/docker-react .
   ```

2. **Push to Docker Hub:**
   ```bash
   docker push pkarczmarczyk/docker-react
   ```

3. **Deploy to AWS EB:**
   - Create application package
   - Upload to Elastic Beanstalk environment

## 🌐 AWS Elastic Beanstalk Configuration

**Application Details:**
- **Application Name**: frontend
- **Environment**: Frontend-env
- **Region**: us-east-2
- **Platform**: Docker

The deployment uses AWS Elastic Beanstalk for easy scaling and management of the containerized application.

## 📚 Learn More

- [Create React App Documentation](https://facebook.github.io/create-react-app/docs/getting-started)
- [React Documentation](https://reactjs.org/)
- [Docker Documentation](https://docs.docker.com/)
- [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
