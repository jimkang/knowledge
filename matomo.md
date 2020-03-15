# Installing

- [Instructions](https://matomo.org/docs/installation/#getting-started)
- The great hassle here is actually getting PHP to work with nginx.
  - After [installing php-fpm](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-in-ubuntu-16-04), these are the nginx config I clawed my way into that actually worked:
    - Move index and root directives up from location blocks up the server block
    - Add under the server block:
        ```location ~ \.php$ {
          # include snippets/fastcgi-php.conf;
          fastcgi_pass unix:/run/php/php7.0-fpm.sock;
          fastcgi_index index.php;
          # include /etc/nginx/fastcgi_params;
          include /etc/nginx/fastcgi.conf;
        }
      location ~ /\.ht {
          deny all;
        }```
   - Some tutorials will have different includes and all sorts of other things under that block. Maybe they work for some environments? They didn't work for me, though.
   - Some things that happened after I initally configured php-fpm:
      - 404 for every php file
        - I think this was actually caused by php-fpm not finding an include?
      - Blank file served for every php file
        - The php extension directive did not apply to the subdirectory under the / location. Hence, I had to move things up.
   - Relevant things to check for debugging:
    - `/var/log/nginx/access.log` of course
    - `/var/log/php7.0-fpm.log`
    - `service php-fpm status`
  - [This Martin Fjordvald article was really helpful for understanding what might be going on.](https://blog.martinfjordvald.com/2011/01/no-input-file-specified-with-php-and-nginx/)
- Then, you'll probable run into permissions errors, but the Matomo PHP page that loads on your server will tell who needs to own what.
- Go through the wizard in the php page.
- [*Sigh* Then, you gotta do the server log stuff](https://matomo.org/docs/log-analytics-tool-how-to/) if, like me, you feel it greatly diminishes the value of Matomo if you have to put in a Google Analytics-style JS tracker.
  - Try: /path/to/piwik/misc/log-analytics/import_logs.py --url=https://yoursite.com/matomo --enable-bots --enable-static --enable-http-errors --enable-reverse-dns --recorders=2 /var/log/nginx/access.log
    - Fix the permissions errors that come up.
    - Adding the user that's going to run this to the `www-data` group will help a lot here.
    - `url` means the URL of your Matomo instance running on PHP, not the site you're tracking.
- Installing Geolocation support
  - `wget https://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz`
  - `tar zxvf GeoLite2-City.tar.gz`
  - `cp GeoLite2-City_20181204/GeoLite2-City.mmdb /path/to/piwik/misc/`
  
# Tracking non-bots

Matomo, when you import logs with `--enable-bots`, will tag visits wit NOT-BOT or BOT, based on user agents that it knows are bots. In practice, that list is always behind. To modify your segment to exclude user agents that you think are bots:
- Edit the segment from the website.
- Add an OR condition.
- Set it to `Browser`, `does not contain`,  and the browser you want to exclude, such as `UC Browser 11.7`.
