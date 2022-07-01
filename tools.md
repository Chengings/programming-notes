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


## Docker

📚
* Official Docker
	* [Tutorial & Samples](https://docs.docker.com/samples/)
	* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
* Dockerfile best practices https://github.com/hexops/dockerfile
* A curated list of Docker Compose samples https://github.com/docker/awesome-compose

### Dockerfile
- Must begin with a `FROM`. ^[https://docs.docker.com/engine/reference/builder/#from]
- Also support `ENV` and `ARG` statements
	- `ENV` is persisted. ^[https://docs.docker.com/engine/reference/builder/#env]
	- `ARG` is not persisted in the final image. ^[https://docs.docker.com/engine/reference/builder/#arg]
- Follow `.dockerignore`. ^[https://docs.docker.com/engine/reference/builder/#dockerignore-file]
- `RUN` command which by default is `/bin/sh -c` on Linux. `RUN` actually runs a command and commits the result.
	- Using pipe: `RUN ["/bin/sh", "-c", "set -o pipefail && wget -O - https://example.com | wc -l > /number"]`
- Only ONE `CMD` instruction in a `Dockerfile`. ^[https://docs.docker.com/engine/reference/builder/#cmd]
	- The main purpose of a `CMD` is to provide **defaults for an executing container**
- 🚧 Do not confuse `RUN` with `CMD`.
- `ENTRYPOINT` should be defined when using the container as an executable. ^[https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact]
- To avoid unintended operations in unknown directories, it is best practice to set your `WORKDIR` explicitly. The `WORKDIR` instruction can be used multiple times in a `Dockerfile`. ^[https://docs.docker.com/engine/reference/builder/#workdir]
- Use case of [`ENTRYPOINT`](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#entrypoint)

[Best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices)
- The container can be stopped and destroyed, then rebuilt and replaced with an absolute minimum set up and configuration.
- Minimise the number of layers. Only the instructions `RUN`, `COPY`, `ADD` create layers.
- Don't install unnecessary packages & use [multi-stage builds])(https://docs.docker.com/develop/develop-images/multistage-build/) (optional: [Distroless](https://github.com/GoogleContainerTools/distroless)).
- Split long or complex `RUN` statements on multiple lines separated with backslashes.
- `CMD` should always be used in the form of `CMD ["executable", "--param1", "--param2"…]`.
- ALWAYS use ABSOLUTE paths for your `WORKDIR`. AVOID `RUN cd … && do-something`, which are hard to read and maintain.
- Strongly encouraged to use `VOLUME` for any MUTABLE or user-serviceable parts of your image, should be used to expose any database storage area, configuration storage, or files/folders.
- If a service **can run without privileges**, use `USER` to change to a non-root user. Start by creating the user and group with something like:  `RUN groupadd -r postgres && useradd --no-log-init -r -g postgres postgres`.
- Although `ADD` and `COPY` are functionally similar, generally speaking, `COPY` **is preferred**. The best use for `ADD` is local tar file auto-extraction into the image, as in `ADD rootfs.tar.xz /`.
- `COPY` them individually, rather than all at once. This ensures that each step’s build cache is only invalidated if the specifically required files change. For example:
```Dockerfile
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY . /tmp/
```

### Install on Pi
1. Follow this guide https://docs.docker.com/engine/install/debian/
2. `sudo pip3 install docker-compose`. Must have python3 and pip3.
3. `sudo systemctl enable docker` to enable docker to system service.

### Exclude sub-folder in volumes
```yml
volumes:
   - /var/cache/
```
https://stackoverflow.com/a/37898591
