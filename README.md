# smee-client dockerized
This is a docker container with smee-client on node:lts-alpine image (i.e. Alpine Linux with NodeJS LTS release).

## Usage

Get smee-client arguments:
```
$ docker run --rm deltaprojects/smee-client

Options:
  -v, --version          output the version number
  -u, --url <url>        URL of the webhook proxy service. Default: https://smee.io/new
  -t, --target <target>  Full URL (including protocol and path) of the target service the events will forwarded to. Default: http://127.0.0.1:PORT/PATH
  -p, --port <n>         Local HTTP server port (default: 3000)
  -P, --path <path>      URL path to post proxied requests to` (default: "/")
  -h, --help             output usage information
```


#### example
Setup smee-client

- Go to https://smee.io/new
- Copy the smee.io **Webhook Proxy URL**, ex *https://smee.io/z3x5DliUZN7GlQqI*
- Run smee-client somwhere it can reach your hosted jenkins, with `-u` argument pointing at the **Webhook Proxy URL** and the `-t` argument pointing at your jenkins webhook url
Ex.
```
docker run -d --name smee-client deltaprojects/smee-client -u https://smee.io/z3x5DliUZN7GlQqI -t https://MY-INTERNAL-JENKINS:8443/github-webhook/
```

Next, configure your GitHub/GitLab/BitBucket webhook, for GitHub:

- Paste in the smee.io **Webhook Proxy URL**, you copied from the step above
- Choose *application/json* as the content type
- Tell it to send the events you want
- Press Add webhook

#### Jenkins example
Aslo setup your Jenkins to work with GitHub or other hosted git service.
For GitHub
- Setup Jenkins [GitHub plugin](https://plugins.jenkins.io/github) (pro tip: Set the *Specify another hook URL for GitHub configuration* to the smee.io Webhook Proxy URL)
- Setup your project/pipeline/whatever...
- Enable the *GitHub hook trigger for GITScm polling* in your project/pipeline..
