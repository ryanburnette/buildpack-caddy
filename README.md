# Heroku Buildpack for Caddy

This is a Heroku Buildpack for [Caddy](https://caddyserver.com).

## Disclaimer

I am experimenting with using Caddy as an injected web server in a Heroku
project, but I'm not sure if it is going to work.

## Installation

```bash
heroku config:add BUILDPACK_URL=https://github.com/ryanburnette/buildpack-caddy.git
```

## Usage

Include `Caddyfile` in your repository.

Heroku apps are not expected to rely on runtime injection of a web server like
Caddy, but the environment does not preclude it and the benefits of configuring
with a Caddyfile are obvious. You won't be able to use Certmagic, however.
You'll need to configure Caddy to listen on the Heroku environment port.

```
http://0.0.0.0:{$PORT} {
  root * dist/
  file_server
  reverse_proxy /api http://127.0.0.1:3001
}
```
