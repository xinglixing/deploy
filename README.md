# deploy

wget -O - https://raw.githubusercontent.com/xinglixing/deploy/master/go.sh | bash

# ssl
* Run sudo nano /etc/nginx/sites-enabled/default
* Add server_name <your-domain/subdomain> directive into "server" group
* Run sudo systemctl restart nginx.service
* Run sudo certbot --nginx -d <your-domain/subdomain> --non-interactive --agree-tos --register-unsafely-without-email
* Run sudo systemctl restart nginx.service
* Run sudo nano /var/www/html/.env
* Change APP_URL= variable content with your https://your-domain/subdomain
* Run cd /var/www/html/
* Run php artisan config:cache

# Custom Nginx
* Run ssh root@<server-ip>
* Run sudo nano /etc/nginx/cipi/<app-user>.conf
* Edit your custom configuration
* Run sudo systemctl restart nginx.service

# Connect a GIT
* Run ssh <app-user>@<server-ip>
* Run rm -rf /home/<app-user>/web (all application web contents will be delete)
* Copy /home/<app-user>/git/deploy.pub into Github SSH Keys
* Run nano /home/<app-user>/git/deploy.sh
* Edit your Git repository name, branch and optional post deploy scripts
* Run sh /home/<app-user>/git/deploy.sh to deploy Git on your server
* You can create a PHP webhook (git ignored) into your /web folder with command with exec commant to deploy.sh

# Supervisor
* Run ssh root@<server-ip>
* Run sudo nano /etc/supervisor/supervisord.conf
* Edit your custom configuration
* Run sudo service supervisor restart

# Cron Jobs
* Run ssh <app-user>@<server-ip>
* Run crontab -e
* Edit your crons

# Local backups
* Run ssh <app-user>@<server-ip>
* Run nano /home/<app-user>/bks/db.sh
* Edit your database informations and set backup retain days
* Run nano /home/<app-user>/bks/fs.sh
* Set backup retain days
* Run sh /home/<app-user>/bks/db.sh to dump your Application database
* Run sh /home/<app-user>/bks/fs.sh to backup your web directory
* Backups are avalable into /bks subdirs. You can use a cron to automate backups
