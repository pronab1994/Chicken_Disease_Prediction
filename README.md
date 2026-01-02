🐔 Chicken Disease Classification (CNN / VGG16)

End-to-end Deep Learning + MLOps project for chicken disease classification using CNN / Transfer Learning (VGG16), integrated with DVC, Docker, and CI/CD pipelines for AWS and Azure.

📌 Project Workflow

Update config.yaml

(Optional) Update secrets.yaml (do not commit secrets)

Update params.yaml

Define entities

Update configuration manager (src/config)

Implement components

Build training & prediction pipelines

Update main.py / app.py

Track pipeline using dvc.yaml

🚀 How to Run the Project
STEP 1: Create Conda Environment
conda create -n cnncls python=3.8 -y
conda activate cnncls

STEP 2: Install Dependencies
pip install -r requirements.txt

STEP 3: Run the Application
python app.py


Then open the application in your browser using the local host and port shown in the terminal.

📊 Data Version Control (DVC)
dvc init
dvc repro
dvc dag

☁️ AWS CI/CD Deployment (GitHub Actions)
1. AWS Setup

Create an IAM user with:

AmazonEC2FullAccess

AmazonEC2ContainerRegistryFullAccess

2. Deployment Flow

Build Docker image

Push image to Amazon ECR

Launch EC2 instance

Pull image from ECR on EC2

Run Docker container on EC2

3. ECR Repository

Create an ECR repository and store the URI securely (do not hardcode credentials).

Example (placeholder):

<aws_account_id>.dkr.ecr.<region>.amazonaws.com/chickendisease

4. Install Docker on EC2
sudo apt-get update -y
sudo apt-get upgrade -y

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker ubuntu
newgrp docker

5. Configure EC2 as Self-Hosted GitHub Runner
Repository → Settings → Actions → Runners → New self-hosted runner

6. GitHub Secrets (Required)

Store all credentials in GitHub Secrets, never in code or README:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
AWS_ECR_LOGIN_URI
ECR_REPOSITORY_NAME

☁️ Azure CI/CD Deployment (GitHub Actions)
Important Security Note

Never store Azure registry passwords or tokens in this repository.
Always use GitHub Secrets, Azure CLI, or Service Principals.


Build & Push Docker Image (Example)
docker build -t <your-registry>.azurecr.io/chicken:latest .

# Recommended (secure)
az acr login -n <your-registry>

# Alternative
docker login <your-registry>.azurecr.io

docker push <your-registry>.azurecr.io/chicken:latest

Azure Deployment Steps

Build Docker image

Push image to Azure Container Registry

Create Azure Web App (Container)

Configure Web App to pull image from ACR

Deploy and run the application
