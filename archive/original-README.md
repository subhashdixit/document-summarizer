# End-to-End Text Summarizer Project

## Introduction

This project provides an end-to-end solution for text summarization using PyTorch. The repository includes setup instructions, usage details, and deployment guidelines using AWS and GitHub Actions.

## Installation and Setup

### Install PyTorch Locally

1. **Install PyTorch**:
   - Visit the [PyTorch Installation Guide](https://pytorch.org/get-started/locally/) for the latest installation commands.
   - Use the following command to install PyTorch with CUDA 11.8 support:
     ```bash
     pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
     ```

2. **Install Visual Studio C++**:
   - Download and install Visual Studio C++ from [Visual Studio](https://visualstudio.microsoft.com/vs/features/cplusplus/).

### Resolve Import Errors

To fix the error "ImportError: Using the `Trainer` with `PyTorch` requires `accelerate>=0.21.0`," follow these steps:

1. **Upgrade Accelerate**:
   ```bash
   pip install --upgrade accelerate
   pip uninstall -y transformers accelerate
   pip install transformers accelerate
   ```

## Project Configuration

### Update Configuration Files

#### Update `config.yaml`

- **Action**: Modify the `config.yaml` file to match your environment and project requirements.
- **Purpose**: Ensures that the configuration settings are tailored to your specific setup and needs.

#### Update `params.yaml`

- **Action**: Adjust the parameters in the `params.yaml` file as needed.
- **Purpose**: Allows you to fine-tune the parameters used in your project to optimize performance and functionality.

#### Update Entity

- **Action**: Review and update the entity definitions if necessary.
- **Purpose**: Ensures that the data entities used in the project are correctly defined and aligned with your current project specifications.

#### Update Configuration Manager

- **Action**: Update the configuration manager in the `src/config` directory.
- **Purpose**: Ensures that the configuration manager is correctly set up to handle configuration files and settings within the source code.

#### Update Components

- **Action**: Make changes to the components as required by the project.
- **Purpose**: Adjust the project components to meet any new requirements or improvements.

#### Update Pipeline

- **Action**: Update the pipeline configuration to reflect any changes in the project setup.
- **Purpose**: Ensures that the data processing and flow through the pipeline are up-to-date with the latest project configuration.

#### Update `main.py`

- **Action**: Apply any necessary changes to the `main.py` script.
- **Purpose**: Ensures that the main script is updated to reflect recent changes in the project or its requirements.

#### Update `app.py`

- **Action**: Modify the `app.py` script according to project needs.
- **Purpose**: Adjust the application script to align with any updates or new features in the project.


## How to Run

### Steps to Run Locally

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/subhashdixit/end_to_end_text_summarization_project
    ```

2. **Create and Activate virtual Environment:**

    ```bash
    ""python3.10 version path"" -m venv venv
    .\venv\Scripts\activate
    ```

3. **Install the Requirements:**

    ```bash
    pip install -r requirements.txt
    ```

4. **Run the Application:**

    ```bash
    python app.py
    ```

5. **Access the Application:**

    Open your web browser and navigate to the local host and port where the application is running.

### Steps for AWS CI/CD Deployment with GitHub Actions

#### AWS Setup

1. **Login to AWS Console**
   - Access your AWS Management Console using your AWS credentials.

2. **Create IAM User for Deployment**
   - **Create User**:
     - Go to the IAM service and create a new user for deployment.
     - Assign the following access permissions:
       - **EC2 Access**: Allows access to EC2 virtual machines.
       - **ECR Access**: Allows saving Docker images to ECR.
     - **AWS Policies**:
       - **AmazonEC2ContainerRegistryFullAccess**
       - **AmazonEC2FullAccess**
   - **Create Access Key**:
     - Navigate to the **Security credentials** tab of the IAM user.
     - Create an access key to use in your GitHub Actions workflow.

   - **Deployment Steps**:
     1. **Build Docker Image**
        - Create a Docker image from your source code using a Dockerfile.

     2. **Push Docker Image to ECR**
        - Push the Docker image to Amazon ECR (Elastic Container Registry).

     3. **Launch EC2 Instance**
        - Launch an EC2 instance where the Docker container will be deployed.

     4. **Pull Docker Image on EC2**
        - Pull the Docker image from ECR to the EC2 instance.

     5. **Run Docker Container on EC2**
        - Run the Docker container on the EC2 instance to start the application.

#### Create ECR Repository

3. **Create ECR Repository**
   - Create an ECR repository to store your Docker image.
   - Save the repository URI: `276333489749.dkr.ecr.ap-south-1.amazonaws.com/textsummarization`

#### Set Up EC2 Machine

4. **Open EC2 and Install Docker**
   - **Optional**: Update and upgrade the EC2 instance.
     ```bash
     sudo apt-get update -y
     sudo apt-get upgrade
     ```
   - **Required**: Install Docker on the EC2 instance.
     ```bash
     curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
     sudo usermod -aG docker ubuntu
     newgrp docker
     ```

5. **Configure EC2 as a Self-Hosted Runner**
   - Go to GitHub **Settings** > **Actions** > **Runners** > **New self-hosted runner**.
   - Choose the operating system and follow the provided commands to set up the runner.

6. **Setup GitHub Secrets**
   - Add the following secrets to your GitHub repository:
     - `AWS_ACCESS_KEY_ID`
     - `AWS_SECRET_ACCESS_KEY`
     - `AWS_REGION`: `ap-south-1`
     - `AWS_ECR_LOGIN_URI`: `276333489749.dkr.ecr.ap-south-1.amazonaws.com`
     - `ECR_REPOSITORY_NAME`: `textsummarization`

### Notes

- **Docker Image Creation**: Ensure your Dockerfile is correctly set up to build your application image.
- **IAM User Permissions**: The IAM user must have the necessary permissions to access ECR and EC2 services.
- **EC2 Configuration**: Verify that Docker is correctly installed and configured on your EC2 instance.
- **Self-Hosted Runner**: Ensure that the EC2 instance is properly set up as a GitHub Actions self-hosted runner for automated deployments.

### Author

**Subhash Dixit**  
Data Scientist  
Email: [subhashdixit17@gmail.com](mailto:subhashdixit17@gmail.com)
