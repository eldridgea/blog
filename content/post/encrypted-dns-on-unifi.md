---
title: Encrypted Cloudflare DNS on UniFi
date: 2023-11-04
hero: "/img/ubiquiti-switch.jpg"
excerpt: Ensuring the entire network uses encrypted DNS.
authors:
  - Eldridge Alexander
---

I wanted to ensure all my home network traffic was using [encrypted](https://en.wikipedia.org/wiki/DNS_over_HTTPS) [DNS](https://en.wikipedia.org/wiki/DNS_over_TLS) to a DNS provider I control, one with filtering and logging capabilities. I talked about the advantages and disadvantages of encrypted DNS [a few years ago at Black Hat](https://www.youtube.com/watch?v=XCnE2o2pfxs).

This is increasingly supported in various hardware and software, however it is still not natively supported in everything, and I also didn't want to have to go around and configure every single device in my place. So I wanted to use traditional DNS in my home network but proxy it at my router, and convert upstream requests to an encrypted DNS protocol.

Proxies like this [exist](https://github.com/eldridgea/dnsonward) and can be pointed at just about any upstream provider, and more vendor-specific software also exists. But I had a couple of constraints[^1]: Use Cloudflare's [Gateway](https://www.cloudflare.com/zero-trust/products/gateway/) product[^2], use their vendor-specific software, run this directly on my [UniFi Dream Router](https://store.ui.com/us/en/products/udr) (UDR), and I wanted to use their Cloudflare-specific proxy.

The UDR runs on a version of Debian -- Cloudflare generally pushes for DNS proxying like this to be done with their [WARP tool](https://blog.cloudflare.com/announcing-warp-for-linux-and-proxy-mode/). However that tool appeared to only be available in binary form, and not compiled for the UDR's `aarch64` architecture. However I remembered that originally they advertised doing this with the `cloudflared` tool which _is_ available for `aarch64`. It is rarely referenced as such in their documentation these days [other than here](https://developers.cloudflare.com/1.1.1.1/encryption/dns-over-https/dns-over-https-client/). So it seems like even if it is officially supported, it's not the recommended path.

[^1]: Somewhat arbitrary ones to be honest. It was mostly about what made my life easiest the day I was working on this.

[^2]: The Gateway product is essentially their [1.1.1.1](https://1.1.1.1/) service, but with additional controls such as logging and filtering, as well as dedicated endpoints for your deployment.

But, I decided to go ahead -- you can download the [cloudflared binary](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) and run it normally. So I enabled SSH on my UDR, and downloaded `cloudfalred` and put it in `/root`. The UDR also uses `systemd` to run services so I needed to make a configuration file so that it would run automatically.  

First, I needed my Cloudflare Gateway DoH endpoint. I'd already signed up for a free tier [Cloudflare account](https://www.cloudflare.com/plans/zero-trust-services/) account, and logged into the [Cloudflare One dashboard](https://one.dash.cloudflare.com/) and grabbed the URL for DNS over HTTPS. This URL is specific to my deployment, so it'll log and filter according to the rules I've set in my Gateway settings.

![Cloudflare Dashboard Screenshot](/img/cloudflare-gateway-screenshot.png)

Once I had that, on the UDR I created the file `/etc/systemd/system/cloudflare-dns-proxy.service` and added the relevant [configuration details](https://gist.github.com/eldridgea/972a894453536a0c0e219b9e3fdcbd96).

Once that file existed, I ran:

1. `systemctl daemon-reload`
1. `systemctl enable cloudflare-dns-proxy.service`
1. `systemctl start cloudflare-dns-proxy.service`

This will add the service, set it to run at boot, and go ahead and turn it on. The service will launch a DNS server running on `127.0.0.53`. That'll be a local service that the UDR can access internally. From there I set that as the "upstream" DNS provider in the UDR's Internet settings.

![UniFi Dashboard Screenshot](/img/udr-cf-dns-screenshot.png)

Once that's done and the settings are saved and changes applied, the network should be encrypting all DNS traffic to Cloudflare! To verify, Cloudflare has [a DNS test page](https://1.1.1.1/help), and so before you're using Cloudflare it may look like this.

![Screenshot of Cloudflare Help Page](/img/1111-not-encrypted.png)

Afterwards, it should look like this! 

![Screenshot of Cloudflare Help Page](/img/1111-encrypted.png)

You can also use this method to leverage other Cloudflare services such as Cloudflare Tunnels. I do that and will write that up at some point too.

I have not tested this, but this method should also work fine with other providers, such as [NextDNS](https://nextdns.io/) other excellent DNS provider with their own vendor tool.
