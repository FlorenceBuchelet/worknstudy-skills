# Nginx

*Env*: Ubuntu.

First installation and use of Nginx as the HTTP server of choice of a PHP project.

> On the software side, a web server includes several parts that control how web users access hosted files. At a minimum, this is an HTTP server. An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages). An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device. [MDN]

Meaning, the HTTP server understands frontend's requests and sends back the correct response. It makes the dialogue possible. CORS management is about authorizing this dialogue.

## Why Nginx?

Nginx is becoming an industry standard and has very good performances though it is not the easiest HTTP server for beginners.

## Install

If you're on Linux, you might want to disable pre-installed Apache2 to avoid conflicts (`sudo systemctl stop apache2` and `sudo systemctl disable apache2`, you will have to `sudo systemctl enable apache2` back later if you want it to auto launch). **Reboot your system.** Then, to start the installation itself, update your system (`sudo apt update`) and install Nginx (`sudo apt install nginx`). It'll run automatically but you can stop it with `sudo systemctl stop nginx.service`, disable auto launch with `sudo systemctl disable apache2` or enable it back. Get informations about Nginx status with `sudo systemctl status nginx.service`.

For Windows you can download Nginx from their website, extract the archive and configure your server. Start command will be, in `C:\nginx`, `start nginx`.

For Mac, you're going to need *Homebrew* (`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`) to install Nginx from your terminal (`brew install nginx`) then you can configure it. Start command will be `sudo nginx`.

## Add Server block (Apache's Virtualhost equivalent)

*Server Blocks* or *Server directives* are an Nginx concept, they configure a port and domain name for a specific project. They allow multiple projects to run on the same Nginx instance.

1. Add your server block in this directory as a .conf file: `/etc/nginx/sites-available/`

    ex. `sudo nano /etc/Nginx2/sites-available/your-project`

    The content is: 
    ```sh
    server {
        listen 80; # You can edit the port to avoid conflicts if needed
        server_name remix-share; # Could be localhost or anything you want

        root /home/your-pc/Desktop/Project/your-project/backend;
        index index.php index.html index.htm;

        location / {
            try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/var/run/php/php8.3-fpm.sock; # Adapt to your version of PHP, verify fpm.sock is installed
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
        }

        error_log /var/log/nginx/remix-share_error.log;
        access_log /var/log/nginx/remix-share_access.log;
    }

    ```
    Other lines take care of authorizations and error handling. Don't forget to delete the comments.

2. If you've changed the **ServerName** from *localhost* to something else, add the new name to your hosts in `/etc/hosts` as `127.0.0.1 your-project` (you need administrator rights to rewrite this).
3. Test Nginx's Configuration with `sudo nginx -t`.

4. Restart Nginx with `sudo systemctl restart Nginx2`.

    ⚠️ Your changes won't be effective if you don't restart Nginx.
    
5. Go to http://your-project/ and admire a beautiful *Index of* page with a list of your project's files or, even better, your index.php showing.


6. ⚠️⚠️ You might need to give permissions to read through your files so Nginx can reach your directory with `chmod +rx /home/your-pc/Desktop/Project/your-project`. Starts with the latest to the first. 

    For example, if your directory is `/home/your-pc/Desktop/Project/your-project`authorize `your-project` first. It should work with only this folder so, for now, go on with the next steps. But if it doesn't, authorize `Project`then `Desktop` ...etc. Until it works. 
    
    For debugging purposes, use `sudo tail -f /var/log/Nginx2/error.log`. It shows Nginx's logs. Check the permissions with `ls -l /home/your-pc/Desktop/Project/your-project`.

    In the `chmod` command, `o` means others as in others users can go through this folder, `+` adds permissions, `r` is reading permission and `x` execute permissions. Add your authorizations as it fits.

    Restart and go to http://your-project/ with each step.


### Common issues encountered: 
- **The page doesn't exist**: host issue (step 2).
- **403 Forbidden**: authorization issue (step 3).


## Edit Nginx port

You can check which port is used with `sudo ss -tulpn`.

1. Go to `/etc/nginx`
2. Edit (you might need to add the line) `nginx.conf` with:
```sh
    HTML {
    (...)
        server {
            listen 8080; # your new port
        }
    (...)
    }
```
3. Edit server ports in all server blocks, including default in `/etc/nginx/sites-available/`.
4. Restart Nginx.