# Creating and connecting to a EC2 Instance using Ubuntu on puTTY

EC2 instance = Virtual server running on AWS (eg. we use it to run backend)

Connect to EC2 using IP address & private key :

- puTTY , a SSH client
- ubuntu
- Remote desktop connection (RDC)

Transfer frontend and backend source code from local to EC2:

- WinSCP
- Git (install git and clone)

Remember to add .env file if necessary

Install database to EC2

```bash
sudo apt install postgresql postgresql-contrib

sudo systemctl start postgresql
sudo systemctl enable postgresql
```

Set up pg user and create database if necessary

# systemd

Use systemd to run application in background

## Frontend

Create frontend.service file

```bash
sudo vim /etc/systemd/system/frontend.service
```

_frontend.service_ file with details for systemd to know how to start up frontend

```bash
[Unit]
Description=To do frontend
After=network.target multi-user.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/to-do-fullstack/frontend
ExecStart=/usr/bin/npm start
Restart=always
Environment=NODE_ENV=production
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=myapp

[Install]
WantedBy=multi-user.target
```

Start frontend service

```bash
sudo systemctl daemon-reload
sudo systemctl enable frontend.service
sudo systemctl start frontend.service
```

```bash
sudo systemctl restart frontend.service
```

See frontend service logs

```bash
sudo journalctl -u frontend.service
```

## Backend

```bash
sudo vim /etc/systemd/system/backend.service
```

```bash
[Unit]
Description=To do backend
After=network.target multi-user.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/to-do-fullstack/backend
ExecStart=/usr/bin/npm run dev
Restart=always
Environment=NODE_ENV=production
EnvironmentFile=/home/ubuntu/to-do-fullstack/backend/.env
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=myapp

[Install]
WantedBy=multi-user.target
```

Start backend service

```bash
sudo systemctl daemon-reload
sudo systemctl enable backend.service
sudo systemctl start backend.service
```

```bash
sudo systemctl restart backend.service
```

See backend service logs

```bash
sudo journalctl -u backend.service
```

**Create .env file** for environment variables
