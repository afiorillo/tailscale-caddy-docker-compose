# Docker Compose template for a service behind Tailscale

Simplifying hosting a service within Docker Compose but making it accessible as its own host in Tailscale.

## Usage

1. Use this repo as a Template, create your own *private* repository.
2. `cp .env.example .env` and modify the `SERVICE_NAME` and `TS_AUTHKEY` as needed. The auth key can be generated [here](https://login.tailscale.com/admin/settings/keys).
3. Update the `web` service in docker compose to whatever you want. By default it hosts a browseable file server in the `www/` directory. The container's port should be port `:8080`.
   1. If the container's port cannot change, then update `serve.json` to match whatever port it does host.
4. Run `docker compose up` and from another node in your tailnet try to access https://example.tail00000.ts.net/ (updating the URL to match your values). The first visit may take a few seconds for the certificate to generate.

## Tips

- When creating the auth key, you probably want to make it Ephemeral by default. This will tell Tailscale to remove the machine from your tailnet shortly after it goes offline. Likewise you may want it to be pre-approved, and to have some ACL tags.
- Tailscale serve isn't very well documented. [This page](https://tailscale.com/kb/1313/serve-examples) has some examples, but none document the JSON format. The example works fine for HTTP services, but for more generic TCP bindings (e.g. iperf3) this will need additional discovery.