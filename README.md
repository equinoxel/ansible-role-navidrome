# laurivan.navidrome

Install navidrome and optionally bonob in docker.

## Requirements

You need a machine with Docker installed.

## Role Variables

All variables are listed below (see also `defaults/main.yml`).

### Navidrome

You can (and should) specify the version of the navidrome image:

```yaml
navidrome.image_version: 'latest'
```

Navidrome needs a place to store its configuration and another to pick up music from:

```yaml
navidrome.config_volume: '/mnt/config-local/navidrome'
navidrome.music_volume: '/mnt/music'
```
If you have multiple folders with music, you should create a parent and build symbolic links to them.

The web interface is available at the following port:

```yaml
navidrome.host_port: 48533
```

### Bonob

If you have e.g. a Sonos system in the house, you may install also Bonob by setting `bonob.enabled` to `true`. the default is:

```yml
bonob.enabled: false
```
You can also specify the bonob image version and the port at which is available:

```yml
bonob.image_version: 'latest'
bonob.host_port: 48534
```

You can change the colors of the bonob icon displayed:

```yml
bonob.icon_color: "beige"
bonob.icon_background: "red"
```
#### Sonos

The sonos-related variables are:

```yml
bonob.sonos.auto_register: 'true'
bonob.sonos.device_discovery: 'true'
bonob.sonos.seed_host: 
bonob.sonos.service_id: "246"
```

If you try sonos autodiscovery and it doesn't work, please:

1. Find the IP of one of the Sonos devices
2. Set `bonob.sonos.seed_host` to that IP
3. Replay the role

You can also add custom clients for streaming:

```yaml
bonob.subsonic.custom_clients: 'audio/flac'
```

For more details, please see the [Bonob documentation](https://github.com/simojenki/bonob).

### Generic

You will need to specify a timezone:

```yml
timezone: 'Europe/Brussels'
```

Otherwise, Bonob will point to *Australia/Melbourne*, which may not be the same as Navidrome.

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

```yml
- name: Example playbook
  hosts: services
  vars:
    bonob.enabled: "true"
  roles:
    - 'laurivan.navidrome'

```

## License

MIT

## Author Information

This role was created in 2022 by [Laur Ivan](https://www.laurivan.com).
