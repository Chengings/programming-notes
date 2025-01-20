# Tools

[Compiler Explorer: An Interactive Online Tool That Shows The Assembly Output Of Compiled Code In Languages Like C++, Rust, And Go](https://compiler-explorer.com/)

[free-for.dev: a list of software (SaaS, PaaS, IaaS, etc.) and other offerings that have free tiers for developers](https://free-for.dev/)

[duckduckgo: JSON Beautifier & Validator](https://duckduckgo.com/?q=json+formatter)

[squoosh: an image compression web app](https://squoosh.app/)

[badssl.com: testing clients against bad SSL configs](https://badssl.com)

[Modern unix tools](https://github.com/ibraheemdev/modern-unix)

## Browser devtools

📚
- Firefox: https://firefox-source-docs.mozilla.org/devtools-user/
- Chrome: https://developer.chrome.com/docs/devtools/
	- https://developer.chrome.com/tags/devtools-tips/
	- https://developer.chrome.com/docs/devtools/console/utilities/
- Edge: https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/landing/
- Safari: https://webkit.org/web-inspector/
- https://devtoolstips.org

### Console helpers

Check [Console API](https://developer.mozilla.org/en-US/docs/Web/API/Console_API) for spec and browser implementations.
- [Firebug command line source](https://github.com/firebug/firebug/blob/master/extension/content/firebug/console/commandLineAPI.js)
- [Chromium console source](https://source.chromium.org/chromium/chromium/src/+/main:v8/src/inspector/v8-console.cc)

`$_`
returns the value of the most recently evaluated expression. For example, if you type “2+2 <enter>”, then “$_ <enter>”, the console will print 4.

`$0`
returns the most recently selected element or JavaScript object.

`$1..$4`
(chrome only) same as `$0` but last four DOM.

`$(selector(, element))`
shortcut for the `document.querySelector()`.]
`element` is optional, default element is `document`.
```js
$('a', document.querySelector('body'))
```

`$$(selector(, element))`
shortcut for the `document.querySelectorAll()`. It returns an array of elements.
```js
console.table(
 $$('a', '.main-content'),
 ['href', 'text']
)

$$('a', $0).map(a => a.href).join('\n')
```
This code is looking for all `<a>` inside elements with the class `.main-content`.  The table will display the `href` (the URL the link points to) and `text` (the visible text within the link) properties of each selected link element.
Check [console.table](https://developer.mozilla.org/en-US/docs/Web/API/Console/table).

`$x(XPath (, element))`
Same as `$$` but use XPath expression.

`clear()`

`copy(arg)`
Copies argument to the clipboard.
```js
copy($0);

copy($$('a').map(a => a.href).join('\n'))

copy($$('a', $0).map(a => a.href).join('\n'))
```

`inspect(obj/func)`
```js
// open in Elements
inspect(document.body);
// open in Source/Debugger
inspect(itIsFunction());
```

`keys()` and `values()`

`monitorEvents(object (, events))`
(chrome only)
```js
monitorEvents(window, "resize");
```

**Firefox only**
`:help`
Go to https://firefox-source-docs.mozilla.org/devtools-user/web_console/helpers/index.html

`:screenshot <filename>`
"filename" is optional, it is not provided output format will be "Screen Shot yyy-mm-dd at hh.mm.ss.png".
Optional parameters:
```
--clipboard
--fullpage
--selector
```

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

### CLI

#### cp

https://docs.docker.com/engine/reference/commandline/cp/

copy files/folders between a container and the local filesystem.

```sh
docker cp container:src_path dest_path|-

docker cp ./some_file container:/work
docker cp container:/var/logs/ /tmp/app_logs 
# The command assumes container paths are relative to the container’s `/` (root) directory, works w/o forward slash.
docker cp container:var/logs/ /tmp/app_logs
```

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

**Distroless**

Repository: https://github.com/GoogleContainerTools/distroless

Distroless images contain only your application and its runtime dependencies. They do not contain package managers, shells or any other programs you would expect to find in a standard Linux distribution.

[Actix-Web in Docker: How to build small and secure images](https://dev.to/sergeyzenchenko/actix-web-in-docker-how-to-build-small-and-secure-images-2mjd) #rust
>Just replace alpine with gcr.io/distroless/cc-debian10 and nothing else. No need to use Musl target. This image contains Libc. The size is 15 Mb larger than alpine, but still small enough.
>
>It’s a good practice to use distroless images in production even if you don't have issues with Musl builds.

[Distroless Containers: Hype or True Value?](https://hackernoon.com/distroless-containers-hype-or-true-value-2rfl3wat)
> However, even for the Go software it can be tricky to run in a scratch container. For example, if you need to process HTTPS traffic, you need to bring the CA certificates yourself. Debugging can also be tricky, because you don’t have a shell to execute, but Docker allows you to start a full fledged debugging container and attach that to the process space of the specimen container
> 
> That said, the distroless trend is absolutely the right direction.
> 
> […]
> 
> We, at Avenga, have used distroless containers in production environments for more than 3 months and are already using multi-stage builds. We weren’t there from the beginning but we were forced, by the security restrictions of our customer to do that. And it worked like a charm (of course with proper orchestration and logging management).
> 
> I can’t say that I am solidly in one of the camps Jacek mentioned above (except for camp 1 :) ) because, as it usually happens in IT, it depends on many factors. But for sure, distroless images are a thing and you definitely should give it a try.


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
