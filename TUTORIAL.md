
### Configuration files

Config files can be in multiple formats, the config file extension must match the format type.
See [example.config.yaml](/example.config.yaml) for a complete example `config.yaml` file.


##### Main settings
```YAML
### Server related settings
address: 0.0.0.0
port: 0
auth: true
# Sets URL prefix for webdav URLs
prefix: /
```


##### TLS / HTTPS settings
If served by a reverse proxy, you can safely leave `tls` as false. It recommended to use TLS on your HTTP server!

```YAML
### Server tls settings
tls: false
cert: cert.pem
key: key.pem
```

##### CORS Settings

```YAML
### CORS configuration
cors:
  enabled: true
  credentials: true
  allowed_headers:
    - Depth
  allowed_hosts:
    - http://localhost:8080
  allowed_methods:
    - GET
  exposed_headers:
    - Content-Length
    - Content-Range
```

##### User defaults
```YAML
# A relative file path that defines where a user's "root" maps to on the real filesystem
path: /
# TODO: Explain this option
scope: .
# Allow Write access
modify: true
# Rule list
rules: []
```

##### Users list - per user credentials and settings
```YAML
users:
  - username: admin
    password: admin
    scope: /a/different/path
    #
  - username: encrypted
    password: "{bcrypt}$2y$10$zEP6oofmXFeHaeMfBNLnP.DO8m.H.Mwhd24/TOX2MWLxAExXi4qgi"
    # use enviroment variable for username and password
  - username: "{env}ENV_USERNAME"
    password: "{env}ENV_PASSWORD"
  - username: basic
    password: basic
    modify:   false
    rules:
      # TODO: Explain these options
      - regex: false
        allow: false
        path: /some/file
      - path: /public/access/
        modify: true
```


### Systemd

An example of how to use this with `systemd` is in [example.webdav.service](/example.webdav.service).


### CORS

The `allowed_*` properties are optional, the default value for each of them will be `*`. `exposed_headers` is optional as well, but is not set if not defined. Setting `credentials` to `true` will allow you to:

1. Use `withCredentials = true` in javascript.
2. Use the `username:password@host` syntax.



### Reverse Proxy Service

When you use a reverse proxy implementation like `Nginx` or `Apache`, please note the following fields to avoid causing `502` errors

##### Nginx
```text
location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header REMOTE-HOST $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }
```

##### Caddy
```Caddyfile
example.com {
	root * /var/www/html
	handle /webdav/* {
		reverse_proxy http://127.0.0.1:8080
    }
}
```