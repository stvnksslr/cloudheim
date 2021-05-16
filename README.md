# cloudheim

kubernetes deployment for a valheim game-server. Based off the docker version by lloesche [here](https://github.com/lloesche/valheim-server-docker).

## Usage

```bash
helm install deploy-name cloudheim/cloudheim  \
  --set valheimServer.serverName="Server Name" \
  --set valheimServer.worldName="World Name" \
  --set valheimServer.serverPass="password" \
  --set valheimServer.serviceType=NodePort \
  --set valheimServer.serverPort=32456 \
  --namespace valheim .
```

## Configuration

Parameter                        | Description                                                                    | Default
:------------------------------- | :----------------------------------------------------------------------------- | :------------------------
`valheimServer.worldName`        | Prefix of the world files to use (will make new if missing)                    | `example-world-name`
`valheimServer.serverName`       | Server name displayed in the server browser(s)                                 | `example-server-name`
`valheimServer.password`         | Server password                                                                | `password`
`valheimServer.serviceType`      | The type of service e.g `NodePort`, `LoadBalancer` or `ClusterIP`              | `ClusterIP`
`valheimServer.nodeSelector`     | this can be used to select a node with specific resources for your game server | `{}`
`valheimServer.serverPublic`     | determines whether the server shows up in the public list or not               | `1`
`valheimServer.updateInterval`   | how often the server checks for updates                                        | `10800` \ 3 hours
`valheimServer.backupsInterval`  | How often the worldfile is backed up                                           | `43200` \ 12 hours
`valheimServer.backupsMaxAge`    | Max age of world file backups kept                                             | `3` \ 3 days
`valheimServer.mods.bepinex`     | whether or not bepinex mod is enabled                                          | `false`
`valheimServer.mods.valheimPlus` | whether or not valheimPlus mod is enabled                                      | `false`
`persistence.claimName`          | if set will not generate a pvc and instead use existing clain                  | ""
`persistence.config.enabled`     | determines if persistence is enabled                                           | `true`
`persistence.config.size`        | size of pvc volume                                                             | `1Gi`
`image.repository`               | Specifies container image repository                                           | `lloesche/valheim-server`
`image.tag`                      | Specifies container image tag                                                  | `latest`

## Connecting to your world

Assuming you have taken care of the networking (port-forwarding if needed, LoadBalancer IP is created, ...):

- In the steam UI (NOT IN GAME) go to view->servers->add favorite

  - set the port to 2457 ([reason for that here](https://github.com/lloesche/valheim-server-docker/discussions/32#discussioncomment-371306))

- To connect double click the server in the steam servers explorer

  - You will be asked for the password in the steam ui and in game

More visual set of instructions [here](https://github.com/mbround18/valheim-docker/discussions/51)
