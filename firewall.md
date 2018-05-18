Setting up the firewall on Ubuntu
----

From [jtittle](https://www.digitalocean.com/community/questions/port-scan-externally-reveals-open-port-from-inside-those-ports-are-closed):

Disable ufw (just to confirm)

    ufw --force disable

Reset ufw

    ufw --force reset

Configure ufw Default Incoming Policy

    ufw default deny incoming

Configure ufw Default Outgoing Policy

    ufw default allow outgoing

Once those settings are in place, you'd want to go about adding the ports that you want to allow in, starting with SSH first so you can connect.

    ufw allow 22/tcp

From there, you'd allow the ports you need for service(s). For example, if we wanted HTTP/S, we'd add 80 and 443.

    ufw allow 80/tcp

    ufw allow 443/tcp

Unless you're using DNS or have a need for udp, most all ports will be tcp, including mail ports.

Once you've added all ports, you'd enable ufw.

    ufw --force enable
