# Caddy Docker with Cloudflare DNS and Docker-Proxy

This Docker image extends the official Caddy image with additional plugins to support Cloudflare DNS and Docker-Proxy functionality.

## Features

- Based on official Caddy Alpine image
- Includes [caddy-docker-proxy](https://github.com/lucaslorentz/caddy-docker-proxy) plugin for automatic Caddy configuration based on Docker labels
- Includes [caddy-dns/cloudflare](https://github.com/caddy-dns/cloudflare) plugin for Cloudflare DNS-01 ACME challenges

## Usage

### Basic Run Command

```bash
docker run -d \
  --name caddy \
  --restart unless-stopped \
  -p 80:80 \
  -p 443:443 \
  -v caddy_data:/data \
  -v /var/run/docker.sock:/var/run/docker.sock \
  your-username/caddy-cloudflare-proxy:latest
```

### Environment Variables

To use the Cloudflare DNS integration, set your API token:

```bash
docker run -d \
  --name caddy \
  -e CLOUDFLARE_API_TOKEN=your-cloudflare-token \
  # other parameters...
  your-username/caddy-cloudflare-proxy:latest
```

### Docker Compose Example

```yaml
version: '3'
services:
  caddy:
    image: your-username/caddy-cloudflare-proxy:latest
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    environment:
      - CLOUDFLARE_API_TOKEN=your-cloudflare-token
    volumes:
      - caddy_data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    
volumes:
  caddy_data:
```

## Building the Image

```bash
docker build -t your-username/caddy-cloudflare-proxy:latest .
```

## License

This project is licensed under the MIT License - see the official [Caddy license](https://github.com/caddyserver/caddy/blob/master/LICENSE) for details.
