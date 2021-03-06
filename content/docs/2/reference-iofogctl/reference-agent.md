# Agent configuration YAML Specification

Agent configuration YAML files let you configure an ioFog Agent provisioned with your Controller.

An Agent configuration can be retrieved using `iofogctl describe agent-config <AGENT_NAME>`

An Agent configuration can be deployed using `iofogctl deploy -f agent-config.yaml`

```yaml
apiVersion: iofog.org/v2
kind: AgentConfig
metadata:
  name: agent-1 # ioFog Agent name
spec:
  # All fields are optional - Only the specified fields will be updated
  name: agent-1
  description: agent running on VM
  latitude: 46.204391
  longitude: 6.143158
  agentType: auto
  dockerUrl: unix:///var/run/docker.sock
  diskLimit: 50
  diskDirectory: /var/lib/iofog-agent/
  memoryLimit: 4096
  cpuLimit: 80
  logLimit: 10
  logDirectory: /var/log/iofog-agent/
  logFileCount: 10
  statusFrequency: 10
  changeFrequency: 10
  deviceScanFrequency: 60
  bluetoothEnabled: true
  watchdogEnabled: false
  abstractedHardwareEnabled: false
  upstreamRouters: ['default-router']
  networkRouter: ''
  host: <Agent_host>
  routerConfig:
    routerMode: edge
    messagingPort: 5672
    edgeRouterPort: 56721
    interRouterPort: 56722
  dockerPruningFrequency: 1
  logLevel: INFO
  availableDiskThreshold: 90
```

| Field                        | Description                                                                                                                                                                                                                                                                                                  |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name                         | User-defined unique identifier of an agent within an ioFog Controller. Must start and end with lowercase alphanumeric character. Can include '-' character.                                                                                                                                                  |
| description                  | Short description of the agent                                                                                                                                                                                                                                                                               |
| latitude                     | Latitude coordinate of the agent. The ioFog Agent will automatically try to detect its own latitude if it has access to the internet                                                                                                                                                                         |
| longitude                    | Longitude coordinate of the agent. The ioFog Agent will automatically try to detect its own longitude if it has access to the internet                                                                                                                                                                       |
| agentType                    | Architecture type of agent. It will be used to determine which image gets deployed. The accepted values are `auto`, `x86` and `arm`. `auto` will have the ioFog agent detect the architecture it is running on, and report it to the ioFog controller. It defaults to `auto` if it fails to parse the value. |
| dockerUrl                    | Docker engine socket                                                                                                                                                                                                                                                                                         |
| diskLimit                    | Limit, in GiB, of disk space that the software is allowed to use                                                                                                                                                                                                                                             |
| diskDirectory                | Set the directory to use for disk storage                                                                                                                                                                                                                                                                    |
| memoryLimit                  | Set the limit, in MiB, of RAM memory that the software is allowed to use for messages                                                                                                                                                                                                                        |
| cpuLimit                     | Set the limit, in percentage, of CPU time that the software is allowed to use                                                                                                                                                                                                                                |
| logLimit                     | Set the limit, in GiB, of disk space that the log files can consume                                                                                                                                                                                                                                          |
| logDirectory                 | Set the directory to use for log file storage                                                                                                                                                                                                                                                                |
| logFileCount                 | Set the number of log files to evenly split the log storage limit                                                                                                                                                                                                                                            |
| statusFrequency              | Set the status update frequency in seconds                                                                                                                                                                                                                                                                   |
| changeFrequency              | Set the get changes frequency in seconds                                                                                                                                                                                                                                                                     |
| deviceScanFrequency          | Set the scan devices frequency in seconds                                                                                                                                                                                                                                                                    |
| bluetoothEnabled             | Boolean. Set on/off for the [bluetooth service](../reference-microserivces-catalog/rest-blue.html). If ON, this will install the restblue microservice                                                                                                                                                       |
| watchdogEnabled              | Boolean. If enabled, watchdog will kill all docker containers running on the agent if they are not part of the microservices deployed by ioFog. If enabled, only docker containers started by the agent process will be allowed to run                                                                       |
| abstractedHardwareEnabled    | Boolean. Set on/off the [HAL services](../reference-microserivces-catalog/hal.html). If ON, this will install the HAL microservice                                                                                                                                                                           |
| upstreamRouters              | Set the upstream routers (using Agent names or `default-router`)                                                                                                                                                                                                                                             |
| networkRouter                | Set the network router (using Agent names or `default-router`)                                                                                                                                                                                                                                               |
| host                         | Hostname used for router communication and public ports. Default: host provided at deploy time.                                                                                                                                                                                                              |
| routerConfig                 | Set the router configuration                                                                                                                                                                                                                                                                                 |
| routerConfig.routerMode      | Set the router mode. Available values are `edge`, `interior` and `none`. Default: `edge`                                                                                                                                                                                                                     |
| routerConfig.messagingPort   | Set the router messaging port. Default: 5672                                                                                                                                                                                                                                                                 |
| routerConfig.edgeRouterPort  | Set the router edge router port. Only valid if routerMode is `interior`. Default: 56721                                                                                                                                                                                                                      |
| routerConfig.interRouterPort | Set the router interior router port. Only valid if routerMode is `interior`. Default: 56722                                                                                                                                                                                                                  |
| logLevel                     | Set the standard logging levels that can be used to control logging output                                                                                                                                                                                                                                   |
| dockerPruningFrequency       | Set the docker pruning frequency in hours                                                                                                                                                                                                                                                                    |
| availableDiskThreshold       | Set the available disk threshold                                                                                                                                                                                                                                                                             |

<aside class="notifications contribute">
  <h3><img src="/images/icos/ico-github.svg" alt="">See anything wrong with the document? Help us improve it!</h3>
  <a href="https://github.com/eclipse-iofog/iofog.org/edit/develop/content/docs/2/reference-iofogctl/reference-agent.md"
    target="_blank">
    <p>Edit this page on Github!</p>
  </a>
</aside>
