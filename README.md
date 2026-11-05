# custom-caddy

GitHub workflow that builds a custom Caddy binary (with [xcaddy](https://github.com/caddyserver/xcaddy)). It checks every 6 hours and builds + publishes a new release whenever Caddy publishes a new version. Each release links to the upstream Caddy release notes. Changing `CADDY_PLUGINS.txt` on `main` also triggers a rebuild, and the workflow can be run manually (with an optional "force" rebuild).

To use as your own, populate `CADDY_PLUGINS.txt` with one plugin per line (blank lines and `#` comments are ignored):

``` bash
$ cat CADDY_PLUGINS.txt
github.com/caddy-dns/cloudflare
github.com/hslatman/caddy-crowdsec-bouncer/http
```

## Rationale

`caddy upgrade` is unreliable and might be removed in the future. This offers a replacement without having to build locally.

The release binary is named `caddy.custom` (with a `caddy.custom.sha256` checksum alongside it):

``` bash
$ wget -q https://github.com/TehNomad/custom-caddy/releases/latest/download/caddy.custom
$ wget -q https://github.com/TehNomad/custom-caddy/releases/latest/download/caddy.custom.sha256
$ sha256sum -c caddy.custom.sha256
$ chmod +x caddy.custom
```
