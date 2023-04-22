# Role vfricou.knot usage

# Tags

| Tag        | Action                                                   |
|------------|----------------------------------------------------------| 
| install    | Perform KNOT authoritative server installation           |
| configure  | Perform KNOT authoritative server and zone configuration |

# Variables

| Name                  | Type   | Default                                   | Comment                                          |
|-----------------------|--------|-------------------------------------------|--------------------------------------------------|
| `knot_listen_address` | Array  | `['127.0.0.1@53']`                        | Define knot server listening addresses and ports |
| `knot_log_base_path`  | String | `'/var/log/knot'`                         | Define knot server logging directory             |
| `knot_log_control`    | Dict   | See [knot_log_control](#knot_log_control) | Define knot server logging for control unit      |
| `knot_log_server`     | Dict   | See [knot_log_server](#knot_log_server)   | Define knot server logging for server unit       |
| `knot_log_zone`       | Dict   | See [knot_log_zone](#knot_log_zone)       | Define knot server logging for zone unit         |
| `knot_log_default`    | Dict   | See [knot_log_default](#knot_log_default) | Define knot server logging for any others logs   |
| `log_retention`       | Int    | `15`                                      | Define logs retentions (in days)                 |
| `knot_zones`          | Dict   | See [knot_zones](#knot_zone)              | Define zones configurations                      |


## knot_log_control
Define target and log level for knot control unit.

Composition :

| Key    | Type    | Default                                     | Comment                |
|--------|---------|---------------------------------------------|------------------------|
| target | String  | `{{ knot_log_base_path }}/knot_control.log` | Log file path for unit |
| info   | String  | `info`                                      | Log level for unit     |

## knot_log_server
Define target and log level for knot server unit.

Composition : 

| Key    | Type    | Default                                    | Comment                |
|--------|---------|--------------------------------------------|------------------------|
| target | String  | `{{ knot_log_base_path }}/knot_server.log` | Log file path for unit |
| info   | String  | `info`                                     | Log level for unit     |

## knot_log_zone
Define target and log level for knot zone unit.

Composition :

| Key    | Type    | Default                                  | Comment                |
|--------|---------|------------------------------------------|------------------------|
| target | String  | `{{ knot_log_base_path }}/knot_zone.log` | Log file path for unit |
| info   | String  | `info`                                   | Log level for unit     |

## knot_log_default
Define target and log level for knot default logging (other units).

Composition :

| Key    | Type    | Default                              | Comment                |
|--------|---------|--------------------------------------|------------------------|
| target | String  | `{{ knot_log_base_path }}/knot.log`  | Log file path for unit |
| info   | String  | `info`                               | Log level for unit     |

## knot_zones

Knot zone dict define zone configurations and entries.  
Zone SOA serial is automatically generated based on epoch time (timestamp).

Example :

```yaml
knot_zones:
  example.org:                                   # Define zone and domain name
    conf:
      ttl: 86400                                 # Define global zone TTL
      contact: 'admin.example.org'               # Define zone contact in SOA
      refresh: '3600'                            # Define SOA refresh value
      retry: '86400'                             # Define SOA retry value
      expire: '86400'                            # Define SOA expire value
      minimum: '3600'                            # Define SOA minimum value
    ns:                                          # Define NS server(s) of zone
      - 'toto.example.org'
    entries:                                     # Define entries of zone
      - '          IN MX 20 mail.example.org.'   # Write each entry in standard format <entry> [TTL] IN <type> <target> 
      - '          IN A 1.2.3.4'                 # Write each entry in standard format <entry> [TTL] IN <type> <target> 
      - 'toto 3600 IN A 1.2.3.4'                 # Write each entry in standard format <entry> [TTL] IN <type> <target> 
      - 'tata      IN CNAME 1.2.3.4'             # Write each entry in standard format <entry> [TTL] IN <type> <target> 
      - 'toto      IN TXT "v=spf1 mx"'           # Write each entry in standard format <entry> [TTL] IN <type> <target> 
```
