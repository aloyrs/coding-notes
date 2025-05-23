# Workflow file

Checkout code to github actions staging repo , npm install , npm run build , rsync to copy over to EC2 instance , restart PM2 and NGINX to see changes

Create workflow file eg.

```bash
name: Deploy to AWS EC2 Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Install frontend dependencies
      run: npm install
      working-directory: frontend

    - name: Build for frontend
      run: npm run build
      working-directory: frontend

    - name: Install backend dependencies
      run: npm install
      working-directory: backend

    # --------------------
    # Deploy to EC2
    # --------------------
    - uses: webfactory/ssh-agent@v0.7.0
      with:
        ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}
    - name: Deploy app to EC2
      run: |
        rsync -avz --exclude "configuration" -e "ssh -o StrictHostKeyChecking=no" -p ./ ${{ secrets.EC2_USERNAME }}@${{ secrets.EC2_HOST }}:/home/ubuntu/to-do-fullstack
    - name: Restart PM2 and Nginx
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.EC2_HOST }}
        username: ${{ secrets.EC2_USERNAME }}
        key: ${{ secrets.SSH_PRIVATE_KEY }}
        port: ${{ secrets.EC2_SSH_PORT }}
        script: |
          sudo pm2 restart 0 --update-env
          sudo pm2 save --force
          sudo rm /etc/nginx/sites-enabled/yomy.online
          sudo ln -s /etc/nginx/sites-available/yomy.online /etc/nginx/sites-enabled/
          sudo systemctl reload nginx
```
