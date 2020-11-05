# localhost.run tunnel as a systemd service

## setup steps

1. Download the `localhost.run.service` file.
1. Rename it to `localhost.run-${domain}@${port}.service`, replacing `${domain}` with either `localhost.run` or your custom domain or subdomain and `${port}` with the local port your webapp listens on for this and all the following steps.  
  hint: You can set env vars, for eg: `domain=example.com port=8080`, for "it just works"™️ copy-pasting action.
1. Create a user systemd folder by running `mkdir -p ~/.config/systemd/user/`.
1. Move your renamed file into `~/.config/systemd/user/`.
1. Run `systemctl --user enable localhost.run-${domain}@${port}.service` to enable your service on startup.
1. Run `systemctl --user start localhost.run-${domain}@${port}.service` to start your service.

The service will generate a key into `~/.ssh/localhost.run.${domain}-${port}.rsa` if one doesn't already exist there.

It writes the tunnels address into `/tmp/localhost.run.${domain}-${port}.address`.

You can check service logs by running `journalctl --user -u localhost.run-${domain}@${port}.service`

PRs are very, very welcome, but pls try to keep the service file as self contained as possible. This means simple commands that exist on most hosts.
