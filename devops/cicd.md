# Manual deployment

Manually deploy to cloud (eg. AWS EC2):

- Create EC2 instance
- SSH in
- Install apps and required software eg. Git , Node
- rsync , scp or git pull files from github
- Use PM2 to run Node backend apps
- Use NGINX to serve frontend pages and redirect api requests to backend port
- Set up env variables
