## Tailscale

What is Tailscale?

Its a vpn tool that allows you to tunnel your devices through the internet without needing to port forward or even poke holes in your firewall, and even bypasses NAT. Is it fast? Yes. Is it free? It is not FOSS but free nonetheless. What is so good about it? Well it isnt protocol-bound and I guess it will be better if you just visit their website and follow the instructions:

[It's right here](https://tailscale.com/)

I tried every other option to connect to my server station remotely for free. Generally, tailscale only allows internal traffic of any kind, but it can be accessed outside using a something very interesting called Tailscale funnel.

Anyhow, tailscale will not work well with the ngrok-systemd service.

It also supports Android/iOS and VMs.

[Help for commands if you're doing this on a server](https://tailscale.com/kb/1080/cli/)
