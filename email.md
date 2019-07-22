# Eeeeeeemail

## Setting up the MTA

(MTA is "mail transfer agent".)

- [MTA comparison](http://shearer.org/MTA_Comparison)
- [Exim](http://www.exim.org/docs.html) might be simpler and better than postfix?
- postfix is installed by default on Ubuntu.
- [Test postfix (via the sendmail command)](http://tombuntu.com/index.php/2009/12/22/send-outgoing-email-with-postfix/) with this command:

    sendmail EMAILADDRESS
    FROM: FROMADDRESS
    SUBJECT: hello world
    this is a test email
    .

(You type each line interactively; sendmail closes when there's a single line with a `.`.)

- When I just ran this without config, my email bounced.
- I edited `/etc/postfix/main.cf` and added this line `notify_classes = resource, software, bounce, policy` then restarted postfix (`service postfix restart` as root or sudo).
- I got this in the log (`/var/log/mail.log`) when sending a test message:

    Jul 21 21:04:00 smallcatlabs-disruption-pod postfix/smtp[19654]: 42AE5DF3AD: to=<jimkang@fastmail.com>, relay=in1-smtp.messagingengine.com[66.111.4.72]:25, delay=1.1,delays=0.02/0.01/1.1/0.02, dsn=5.5.2, status=bounced (host in1-smtp.messagingengine.com[66.111.4.72] said: 504 5.5.2 <root@smallcatlabs-disruption-pod>: Sender address rejected: need fully-qualified address (in reply to RCPT TO command))
