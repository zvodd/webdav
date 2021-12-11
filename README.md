# webdav

![Build](https://github.com/hacdias/webdav/workflows/Tests/badge.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/hacdias/webdav?style=flat-square)](https://goreportcard.com/report/hacdias/webdav)
[![Version](https://img.shields.io/github/release/hacdias/webdav.svg?style=flat-square)](https://github.com/hacdias/webdav/releases/latest)
[![Docker Pulls](https://img.shields.io/docker/pulls/hacdias/webdav)](https://hub.docker.com/r/hacdias/webdav)

## Install

Please refer to the [Releases page](https://github.com/hacdias/webdav/releases) for more information. There, you can either download the binaries or find the Docker commands to install WebDAV.

## Usage

```webdav``` command line interface is really easy to use so you can easily create a WebDAV server for your own user. By default, it runs on a random free port and supports JSON, YAML and TOML configuration. An example of a YAML configuration with the default configurations:

```yaml
# Server related settings
address: 0.0.0.0
port: 0
auth: true
prefix: /

users:
  - username: user
    password: password
    scope: .

```

There are more ways to customize how you run WebDAV through flags and environment variables. Please run `webdav --help` for more information on that.

### Tutorial

Please see [TUTORIAL.md](TUTORIAL.md) for:
  * config.yaml example
  * Configuration value explanations
  * Systemd webdav.service file example
  * CORS header settings and explinations for webdav config file
  * Reverse Proxy example configs for Nginx and Caddy


## License

MIT © [Henrique Dias](https://hacdias.com)
