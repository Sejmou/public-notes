This is done via the `daemon.json` file

On Linux, config file is expected to be located at `/etc/docker/daemon.json` (need to create it if it doesn't exist!)

See also [docs](https://docs.docker.com/engine/reference/commandline/dockerd/#on-linux)

## Applying changes
You need to restart the Docker daemon service! With `systemctl` this can be done by

```bash
sudo systemctl daemon-reload # Reload systemd configuration
sudo systemctl restart docker # Restart Docker service
```

## If larger mounted volume available: change `data-root`
Overrides the default location (`/var/lib/docker`)

```json
{
  "data-root": "/data/docker"
}
```

## Log-rotation (save disk space!)
IMPORTANT: It is apparently pretty difficult to change the log configuration of existing containers! Might be simpler to just create new ones.

Easiest fix to improve logging _for new containers_: change log-driver to `"local"`!
 - adds log rotation per default
 - more memory efficient than default JSON logging

```json
{
  "log-driver": "local"
}
```