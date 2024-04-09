# nginx-2420 - Part1

## Instruction

1. `cd /usr/share/nginx` to go to directory where we save the index.html file

2. `sudo mkdir -p /web/html/nginx-2420`

3. Go to the directory we just created.
Once you got there `vim index.html` to create the HTML file that will be loaded by nginx
Copy and paste these lines of code to `index.html`
    ```
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>2420</title>
        <style>
            * {
                color: #db4b4b;
                background: #16161e;
            }
            body {
                display: flex;
                align-items: center;
                justify-content: center;
                height: 100vh;
                margin: 0;
            }
            h1 {
                text-align: center;
                font-family: sans-serif;
            }
        </style>
    </head>
    <body>
        <h1>All your base are belong to us</h1>
    </body>
    </html>
    ``` 

4. `cd /etc/nginx` to go to configuration folder of nginx

5. First of all, we need to disable and stop the previous nginx service by commands `sudo systemctl stop nginx.service` and `sudo systemctl disable nginx.service`

6. To setup a new server block in seperated file (new server setup is not a part of nginx.conf), we use the pair of `sites-available` and `sites-enabled` folder by commands `sudo mkdir /etc/nginx/sites-available` and `sudo mkdir /etc/nginx/sites-enabled`

7. Create a config file in `sites-available` folder by command `sudo vim sites-available/ass3.conf`
This is script for `ass3.conf`
    ```
    server {
        listen 80;
        server_name localhost;

        location / {
            root /usr/share/nginx/web/html/nginx-2420;
            index index.html index.html;
        }
    }
    ```

8. `ln -s /etc/nginx/sites-available/ass3.conf /etc/nginx/sites-enabled/ass3.conf` to create a symbolic link from `ass3.conf` in `sites-available` folder to `sites-enabled` folder named `ass3.conf`

9. `vim sudo nginx.conf` to start config the nginx config file
- Change the port of default server (which currently using port 80) to whatever port you want (124 for example)
- On the bottom of `html` block, add `include sites-enabled/*;`

10. Now, everything is all set. 
Do `sudo systemctl start nginx.service` and `sudo systemctl enable nginx.service` to start and enable the server again
- Try `systemctl status nginx.service` to check if any errors occur (I expect that no error will appear)

11. Copy the IP Address of the Droplet and this is what I got (the image i provided)