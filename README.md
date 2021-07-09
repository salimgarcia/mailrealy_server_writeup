# MailRelay Server Writeup
Task Description: Look into creating a mailrelay VM. We will use this in later tasks for sending out automated emails.
You should be able to use your work email for the relay. There are a lot of good walk-throughs, but this can be a complicated task, and there are a lot of small, hard to notice, places where it can go wrong. Don't hesitate to ask for help if you get stuck here.

- Set up new Windows Server 2019 VM using the template
- Give the server a static IP and connect it to the domain
- In Server Manager, click `Manage` and select `Add Roles and Features`
- Go to the Features tab and check the `SMTP` feature
- Click next and then click install
- Close the wizard and click on tools and select `IIS 6.0 Manager`
- Click on your machine and then right click `SMTP Virtual Server #1` and select `Properties`
- Check the box for `Enable Logging`, and then click on the `Access` tab
- Click on `Authentication` and make sure `Anonymous Access` is enabled
- Go back to the Access tab and click on `Connection`
- Click `Only the list below` and add the IP addresses of the machines you want to allow to relay email through this server, then click OK
- Click on the `Messages` tab and enter your email address to receive non-delivery reports
- Click on the `Delivery` tab and click the `Outbound Security` button
- Select `Basic Authentication` and enter your email address and app password, then check `TLS encryption` and click OK
- Click `Outbound connections` and for the TCP port enter `587` and click OK
- Click `Advanced` and in `Fully-qualified domain name` enter the name of your domain
- For smart host enter `smtp.gmail.com` and click OK
- Open firewall settings, click advanced, and make sure port 587 is open for outbound connections
- Save the SMTP server settings and restart the server
- Open Powershell and set `smtpsvc` to start automatically when booting the server by running the command `set-service smtpsvc -StartupType Automatic`
- Then start the service by running `start-service smtpsvc`
