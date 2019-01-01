# Adding SSL via Let's Encrypt

- Install [certbot](https://certbot.eff.org/docs/using.html#certbot-commands)
- Update the nginx config with a server block for your domain. (Certbot won't work if you don't do this first.)
- Get a certificate: `certbot run -d yourdomain.com --nginx`
- Diff the changes certbot made to your nginx config against the one you have checked in; revert stuff you don't like.
