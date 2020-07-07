# conditional NGINX logging

> example `nginx.conf` to conditionally log detailed SSL cipher information

## quickstart

```sh
$ hostctl add domains nginx-demo nginx.loc

$ mkcert -cert-file nginx.loc.crt -key-file nginx.loc.key nginx.loc 127.0.0.1

$ docker-compose up -d
```

## example output

### TLSv1.0

#### request

```sh
❯ curl -s https://nginx.loc:10443 --tlsv1.0 | jq
{
  "sslProtocol": "TLSv1",
  "sslCipher": "ECDHE-RSA-AES256-SHA",
  "sslCiphers": "ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-SHA:AES128-SHA:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

#### log output

```javascript
{
  "msec": "1594065308.279",
  "remoteAddr": "172.30.0.1",
  "request": "GET / HTTP/2.0",
  "status": "200",
  "httpUserAgent": "curl/7.58.0"
}
{
  "msec": "1594065308.279",
  "request": "GET / HTTP/2.0",
  "httpUserAgent": "curl/7.58.0",
  "sslProtocol": "TLSv1",
  "sslCipher": "ECDHE-RSA-AES256-SHA",
  "sslCiphers": "ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-SHA:AES128-SHA:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

### TLSv1.1

#### request

```sh
❯ curl -s https://nginx.loc:10443 --tlsv1.1 | jq
{
  "sslProtocol": "TLSv1.1",
  "sslCipher": "ECDHE-RSA-AES256-SHA",
  "sslCiphers": "ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-SHA:AES128-SHA:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

#### log output

```javascript
{
  "msec": "1594065344.991",
  "remoteAddr": "172.30.0.1",
  "request": "GET / HTTP/2.0",
  "status": "200",
  "httpUserAgent": "curl/7.58.0"
}
{
  "msec": "1594065344.991",
  "request": "GET / HTTP/2.0",
  "httpUserAgent": "curl/7.58.0",
  "sslProtocol": "TLSv1.1",
  "sslCipher": "ECDHE-RSA-AES256-SHA",
  "sslCiphers": "ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-SHA:AES128-SHA:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

### TLSv1.2

#### request

```sh
❯ curl -s https://nginx.loc:10443 --tlsv1.2 | jq
{
  "sslProtocol": "TLSv1.2",
  "sslCipher": "ECDHE-RSA-AES256-GCM-SHA384",
  "sslCiphers": "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:DHE-RSA-AES256-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

#### log output

```javascript
{
  "msec": "1594065398.612",
  "remoteAddr": "172.30.0.1",
  "request": "GET / HTTP/2.0",
  "status": "200",
  "httpUserAgent": "curl/7.58.0"
}
```

### TLSv1.3

#### request

```sh
❯ curl -s https://nginx.loc:10443 --tlsv1.3 | jq
{
  "sslProtocol": "TLSv1.3",
  "sslCipher": "TLS_AES_256_GCM_SHA384",
  "sslCiphers": "TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_128_GCM_SHA256:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

#### log output

```javascript
{
  "msec": "1594065440.074",
  "remoteAddr": "172.30.0.1",
  "request": "GET / HTTP/2.0",
  "status": "200",
  "httpUserAgent": "curl/7.58.0"
}
```

### TLS1.x

#### request

```sh
❯ curl -s https://nginx.loc:10443 --tlsv1 | jq
{
  "sslProtocol": "TLSv1.3",
  "sslCipher": "TLS_AES_256_GCM_SHA384",
  "sslCiphers": "TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_128_GCM_SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:DHE-RSA-AES256-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:TLS_EMPTY_RENEGOTIATION_INFO_SCSV"
}
```

#### log output

```javascript
{
  "msec": "1594065480.242",
  "remoteAddr": "172.30.0.1",
  "request": "GET / HTTP/2.0",
  "status": "200",
  "httpUserAgent": "curl/7.58.0"
}
```
