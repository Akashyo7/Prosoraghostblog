Ghost on Fly.io

Apps:
- prosora-ghost (this app): Ghost 6 container with persistent volume
- prosora-proxy: Caddy reverse proxy that terminates TLS and routes ActivityPub endpoints
- prosora-activitypub: TryGhost/ActivityPub service
- prosora-mysql: MySQL database

Secrets to set on prosora-ghost:
- database__connection__password
- (optional) mail__options__auth__pass
- (optional) TINYBIRD_TRACKER_TOKEN
- (optional) TINYBIRD_ADMIN_TOKEN

Volumes:
- fly volumes create ghost_data -a prosora-ghost -r iad -s 10

Deploy:
- fly apps create prosora-ghost
- fly launch --no-deploy (or copy deploy/ghost/fly.toml to app)
- fly volumes create ghost_data -a prosora-ghost
- fly secrets set database__connection__password=... -a prosora-ghost
- fly deploy -a prosora-ghost

Health:
- fly status -a prosora-ghost