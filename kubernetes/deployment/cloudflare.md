# Cloudflare

## Install `Cloudflared` on Ubuntu

1. Add `Cloudflare`'s package signing key
```bash
sudo mkdir -p --mode=0755 /usr/share/keyrings
curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | sudo tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null
```

2. Add `Cloudflare`'s apt repo to your apt repositories

```bash
echo "deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared any main" | sudo tee /etc/apt/sources.list.d/cloudflared.list
```

3. Update repositories and install `cloudflared`
```bash
sudo apt-get update && sudo apt-get install cloudflared
```

## Create a tunnel

1. Login to cloudflare
```bash
cloudflared tunnel login
```

2. Create a tunnel
```bash
cloudflared tunnel create [tunnel name]
```

3. Copy tunnel id for future reference
