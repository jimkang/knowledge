Installing goaccess on Ubuntu
====

- As root: 
  - `apt-get install goaccess`
  - `vi /etc/goaccess.conf`
    - Set the following properties:
      - `time-format %H:%M:%S`
      - `date-format %d/%b/%Y`
      - `log-format %h %^[%d:%t %^] "%r" %s %b "%R" "%u"`
  - Run `goaccess -f /var/log/nginx/access.log -c | more` and make sure you get a report.
  - `adduser <user that'll run the reports> <group for users that should be able to see the logs>
  - From `/var/log`: `chown :<group for users that should be able to see logs>` nginx
  - From `/var/log/nginx`: `chown :<group for users that should be able to see logs>` *
- As <user that'll run the reports>:
  - Run `goaccess -f /var/log/nginx/access.log` and make sure you get a report.
  - `mkdir -p /usr/share/nginx/html/where-you-want-it-to-go/log-reports`
  - Try `zcat /var/log/nginx/access.log.*.gz | goaccess -o test2 > test2.html` and make sure it makes a report that includes all the gzipped logs.
  - Try `goaccess -f /var/log/nginx/access.log -o whatever > test.html` and make sure it makes a report with just access.log. 
  TODO: cron!
  
