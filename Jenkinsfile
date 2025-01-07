pipeline:
  agent: any

  environment:
    DEPLOY_DIR: "directory" 
    GITHUB_REPO: "github_repo"  
    EC2_HOST: "host"  
    EC2_USER: "ec2_user" 
    SSH_KEY_PATH: "automation.pem" 

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
