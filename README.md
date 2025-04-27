# Docker Compose template for a service behind Tailscale

Simplifying hosting a service within Docker Compose but making it accessible as its own host in Tailscale.

## Usage

1. Use this repo as a Template, create your own *private* repository.
2. `cp .env.example .env` and modify the `SERVICE_NAME` and `TS_AUTHKEY` as needed. The auth key can be generated [here](https://login.tailscale.com/admin/settings/keys).
3. Update the `web` service in docker compose to whatever you want. By default it hosts a browseable file server in the `www/` directory. The container's port should be port `:8080`.
   1. If the container's port cannot change, then update `serve.json` to match whatever port it does host.
4. Run `docker compose up` and from another node in your tailnet try to access https://example.tail00000.ts.net/ (updating the URL to match your values). The first visit may take a few seconds for the certificate to generate.
