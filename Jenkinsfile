pipeline:
  agent: any

  environment:
    DEPLOY_DIR: "directory"  # Path where your HTML files are deployed on the EC2 instance
    GITHUB_REPO: "github_repo"  # URL of your GitHub repository
    EC2_HOST: "host"  # Public IP address of your EC2 instance
    EC2_USER: "ec2_user"  # EC2 username
    SSH_KEY_PATH: "automation.pem"  # Path to your private SSH key for accessing the EC2 instance

  stages:
    - stage: Checkout
      steps:
        - script: |
            git branch: "main"
            url: "${GITHUB_REPO}"

    - stage: Build
      steps:
        - script: |
            echo "Building the HTML website..."

    - stage: Deploy
      steps:
        - script: |
            scp -i "${SSH_KEY_PATH}" -r * "${EC2_USER}@${EC2_HOST}:${DEPLOY_DIR}"

  post:
    success:
      - echo: "Deployment was successful!"
    failure:
      - echo: "Deployment failed."
