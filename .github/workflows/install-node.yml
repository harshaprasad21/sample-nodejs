name: Install Node.js on EC2

on:
  workflow_dispatch:  # Allows manual triggering

jobs:
  install-node:
    runs-on: ubuntu-latest

    steps:
    - name: Setup SSH Key
      run: |
        mkdir -p ~/.ssh
        echo "${{ secrets.SSH_PRIVATE_KEY }}" > ~/.ssh/id_rsa
        chmod 600 ~/.ssh/id_rsa
        ssh-keyscan -H ${{ secrets.EC2_HOST }} >> ~/.ssh/known_hosts

    - name: Install Node.js on EC2
      run: |
        ssh -i ~/.ssh/id_rsa ${{ secrets.EC2_USER }}@${{ secrets.EC2_HOST }} << 'EOF'
          echo "Connected to EC2"
          
          # Install Node.js (Ubuntu/Debian)
          curl -fsSL https://deb.nodesource.com/setup_18.x | sudo bash -
          sudo apt install -y nodejs
          sudo npm install 
          sudo npm install -g pm2 

          # Verify installation
          node -v
          npm -v
          
          echo "Node.js installation complete"
        EOF
