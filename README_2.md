# nginx-2420 - Part2

## Table of Contents

## Installation

`sudo pacman -S ufw`

## Instruction

### Firewall

1. Enable UFW: `sudo ufw enable`
2. Allow SSH: `sudo ufw allow ssh`
3. Allow HTTP: `sudo ufw allow http`
4. Allow HTTPS: `sudo ufw allow https`
5. To check: `sudo ufw status numbered`

### Service

1. Place backend binary on your system \
**Step**
- Open the terminal, go to `Downloads` directory and do `git clone https://gitlab.com/cit2420/2420_notes_w24.git`
- `sftp tuan` because i set my name is `tuan`
- `put C:\Users\alext\Downloads\2420_notes_w24\attachments\hello-server`
- `exit` to exit sftp
*Now, i have `hello-server` file in my home directory*

2. Create a new service file to run the backend
- `sudo mv hello-server /web/html/nginx-2420/`
- `cd /web/html/nginx-2420` and `sudo chmod +x hello-server` to make the backend file executable
- `sudo vim /etc/systemd/system/backend.service` to create a new service
- put these commands to the service file
``` bash
[Unit]
Description=Backend Service
After=network.target

[Service]
ExecStart=/web/html/nginx-2420/hello-server
Restart=always

[Install]
WantedBy=multi-user.target
```
- `sudo systemctl daemon-reload`
- `sudo systemctl enable --now backend`
- `sudo systemctl status backend`

3. Edit nginx server block, add reverse proxy to backend
- `sudo rm /etc/nginx/sites-enabled/nginx-2420` 
- `sudo vim /etc/nginx/sites-available/nginx-2420` and add these code to what we already have
``` bash
location /hey {
    proxy_pass http://127.0.0.1:8080;
}

location /echo {
    proxy_pass http://127.0.0.1:8080;

}
```
- `sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/nginx-2420`
- Restart the server and run the nginx again.