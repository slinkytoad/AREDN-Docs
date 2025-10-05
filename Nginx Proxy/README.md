## nginx proxy 

This file is going to live on the proxy that we have configured to send traffic from the public internet to the private network.

This config proxies the data over Tailscale.

You will need to setup certbot before this will work.

- make sure `snapd` is installed before beginning, this should already be done on a Ubuntu system.
- Install certbot: `sudo snap install --classic certbot`
- Link certbot into PATH: `sudo ln -s /snap/bin/certbot /usr/bin/certbot`

From here you need to request the cert for the server. Certbot can configure NGINX on it's own, but i've never had good luck with it working.

- Ensure you have dns records pointing to the proxy server.
- ensure you have the ports open in the firewall for the proxy server, `80` and `443`.
- Stop NGINX: `sudo systemctl stop nginx`
- Get a standalone cert: `sudo certbot certonly --standalone`, and follow the prompts that it will ask.
- Edit the nginx config for the `ssl_certificate` and `ssl_certificate_key` lines to have your domain in the path instead of the example domain.
- run `sudo nginx -T` to test the config
- if the config is good, run `sudo systemctl start nginx` to start nginx again.
- you will want to run the following to allow certbot to stop nginx and reload nginx before and after renewing the cert.

```bash
block for that code
```