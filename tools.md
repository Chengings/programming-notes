# Tools

[curl.trillworks.com: convert curl syntax to Python, Ansible URI, Node.js, R, PHP, Strest, Go, Dart, JSON, Rust](https://curl.trillworks.com/)

[free-for.dev: a list of software (SaaS, PaaS, IaaS, etc.) and other offerings that have free tiers for developers](https://free-for.dev/)

[duckduckgo: JSON Beautifier & Validator](https://duckduckgo.com/?q=json+formatter)

[squoosh: an image compression web app](https://squoosh.app/)

[badssl.com: testing clients against bad SSL configs](https://badssl.com)

[Modern unix tools](https://github.com/ibraheemdev/modern-unix)

## Browser devtools

### Local Overrides
Local overrides allow *permanent change* in local development. It will be remained on page reload and affected in every tab.

Edge or chromium-based browser https://docs.microsoft.com/en-gb/microsoft-edge/devtools-guide-chromium/javascript/overrides

Webkit: it also has features to override request and response.
https://webkit.org/web-inspector/local-overrides/


## DNS

📚
* How to install DNSCrypt-Proxy on Linux with Pi-hole guid https://github.com/pi-hole/pi-hole/wiki/DNSCrypt-2.0

## Docker

📚
* Dockerfile best practices https://github.com/hexops/dockerfile
* A curated list of Docker Compose samples https://github.com/docker/awesome-compose
* Tutorial & Samples https://docs.docker.com/samples/

## Install on Pi
1. Follow this guide https://docs.docker.com/engine/install/debian/
2. `sudo pip3 install docker-compose`. Must have python3 and pip3.
3. `sudo systemctl enable docker` to enable docker to system service.

### Exclude sub-folder in volumes
```yml
volumes:
   - /var/cache/
```
https://stackoverflow.com/a/37898591
