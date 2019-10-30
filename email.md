# Eeeeeeemail

Kind of a verbose version of this document: [Setting up an automated mailing list saga](https://jimkang.com/weblog/articles/running-your-own-email-server/)
## Setting up the MTA

(MTA is "mail transfer agent".)

- [MTA comparison](http://shearer.org/MTA_Comparison)
- [Exim](http://www.exim.org/docs.html) might be simpler and better than postfix?
- postfix is installed by default on Ubuntu.
- [Test postfix (via the sendmail command)](http://tombuntu.com/index.php/2009/12/22/send-outgoing-email-with-postfix/) with this command:

        $ sendmail EMAILADDRESS
        FROM: FROMADDRESS
        SUBJECT: hello world
        this is a test email
        .

(You type each line interactively; sendmail closes when there's a single line with a `.`.)

- When I just ran this without config, my email bounced.
- I edited `/etc/postfix/main.cf` and added this line `notify_classes = resource, software, bounce, policy` then restarted postfix (`service postfix restart` as root or sudo).
- I then did some of [this DNS setup](https://www.c0ffee.net/blog/mail-server-guide/#overview). I only created the A record for the mail domain, the MX record to point to that mail domain, and a TXT record containing `v=spf1 mx -all`. 
- I got this in the log (`/var/log/mail.log`) when sending a test message with a sendmail one-liner that did not set the FROM field:

    Jul 21 21:04:00 smallcatlabs-disruption-pod postfix/smtp[19654]: 42AE5DF3AD: to=<jimkang@fastmail.com>, relay=in1-smtp.messagingengine.com[66.111.4.72]:25, delay=1.1,delays=0.02/0.01/1.1/0.02, dsn=5.5.2, status=bounced (host in1-smtp.messagingengine.com[66.111.4.72] said: 504 5.5.2 <root@smallcatlabs-disruption-pod>: Sender address rejected: need fully-qualified address (in reply to RCPT TO command))

- After using the interactive version above, sending email worked!
- However, email sent to Gmail bounced, probably because I did not have a [reverse DNS record](https://support.google.com/mail/answer/81126#authentication) set up.
- After setting up a reverse DNS record (PTR) by renaming the droplet in Digital Ocean to match the hostname, email did make it Gmail, though it did get classified as spam.
- Incoming mail did not work until I:
    - Ran `ufw allow 25` to make sure port 25 was open to the world. (I neglected to check whether it was closed before I ran this, so it may not have mattered in this case.)
    - Properly included my domain in `mydestination` in `/etc/postfix/mail.cf`. Before, I had `mail.smidgeo.com`, even though the mail is actually addressed to `@smidgeo.com`.

## Installing GNU Mailman

Mailman is a mailing list manager.

[This post explains really well how to set it up.](http://jhshi.me/2014/11/16/mailman-configuration-with-nginx-plus-fastcgi-plus-postfix-on-ubuntu/index.html)

Disappointingly, Mailman sends people's passwords to them in plain text and has a cumbersome UI for subscribers.

However, by setting the "mod" checkbox for each user, they can be disallowed from post directly to the list, which is a nice feature.

## Vacation

`vacation` is a simple program for autoreplying.

- Very important to have the `-r 0` switch for the vacation command in .forward if you're going to reply more than once per day.
- `vacation -l` lists all of the emails it responded to and when.
- Does not give you control over whether you reply to the Reply-To or From fields of an incoming message.