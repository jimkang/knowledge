# Installing awstats for nginx

- `apt-get install awstats`
- `cd /etc/awstats`
- Edit `awstats.conf` with the following updates:
    - `LogFile="/var/log/nginx/access.log"
    - `SiteDomain="smidgeo.com"`
- Edit `/etc/logrotate.d/nginx.conf` like so:
```
    /var/log/nginx/*.log {
        daily # rotate daily
        missingok 
        rotate 52 # Keep 52 days
        compress
        delaycompress
        notifempty
        create 0640 www-data adm
        sharedscripts
        prerotate
                # Trigger awstats computation
                /usr/share/doc/awstats/examples/awstats_updateall.pl now -awstatsprog=/usr/lib/cgi-bin/awstats.pl
        endscript
        postrotate
                # Reload Nginx to make it read the new log file
                [ ! -f /var/run/nginx.pid ] || kill -USR1 `cat /var/run/nginx.pid`
        endscript
    }
```
- Run `/usr/share/doc/awstats/examples/awstats_updateall.pl now -awstatsprog=/usr/lib/cgi-bin/awstats.pl`
- Build HTML with `/usr/share/awstats/tools/awstats_buildstaticpages.pl -config=awstats.conf -awstatsprog=/usr/bin/awstats -dir=/usr/share/nginx/html/smidgeo.com/<dir>`
- Add the HTML build command to cron.

The above worked. Mostly based on [this](https://kamisama.me/2013/03/20/install-configure-and-protect-awstats-for-multiple-nginx-vhost-on-debian/).
