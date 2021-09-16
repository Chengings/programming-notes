# Tools

[Convert curl syntax to Python, Ansible URI, Node.js, R, PHP, Strest, Go, Dart, JSON, Rust](https://curl.trillworks.com/)

[Open Source macOS apps](https://internetprivacyguy.com/list-of-open-source-macos-apps/)

[a list of software (SaaS, PaaS, IaaS, etc.) and other offerings that have free tiers for developers](https://free-for.dev/)

[JSON Beautifier & Validator](https://duckduckgo.com/?q=json+formatter)

[Squoosh: an image compression web app](https://squoosh.app/)

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
