pipeline:
  agent any

  environment:
    # Define environment variables for SSH key, EC2 instance IP, and path to your HTML project
    EC2_INSTANCE: "ec2-user@<EC2_PUBLIC_IP>"
    SSH_KEY_PATH: "/path/to/your/ssh/key.pem"  # Make sure to use your Jenkins' SSH key location

  stages:
    - stage: "Login to EC2 and Pull HTML Project"
      steps:
        script:
          # Log in to the EC2 instance and pull/build the HTML project
          sh """
            echo 'Logging in to EC2 instance...'
            ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${EC2_INSTANCE} << EOF
            cd /var/www/html/mywebsite || mkdir -p /var/www/html/mywebsite
            # Pull or build the HTML site (assuming Git is installed and repo is available)
            git clone https://github.com/your-repo/html-site.git .
            # Or if you're building the HTML, replace the git pull with your build steps
            # Example: npm run build (if it's a JS app)
            EOF
          """

    - stage: "Deploy HTML Site"
      steps:
        script:
          # Deploy HTML site (this could just be pulling the HTML or starting a server like nginx)
          sh """
            echo 'Deploying HTML site on EC2 instance...'
            ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${EC2_INSTANCE} << EOF
            # Install necessary packages if required, like nginx
            sudo apt-get update
            sudo apt-get install -y nginx
            sudo systemctl restart nginx
            EOF
          """

    - stage: "Finish"
      steps:
        script:
          echo "HTML site deployed successfully!"
