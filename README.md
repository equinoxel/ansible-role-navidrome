# laurivan.navidrome

Install navidrome and optionally bonob in docker.

## Requirements

You need a machine with Docker installed.

## Role Variables

All variables are listed below (see also `defaults/main.yml`).

### Navidrome

You can (and should) specify the version of the navidrome image:

```yaml
navidrome_image_version: 'latest'
```

Navidrome needs a place to store its configuration and another to pick up music from:

```yaml
navidrome_config_volume: '/mnt/config-local/navidrome'
navidrome_music_volume: '/mnt/music'
```
If you have multiple folders with music, you should create a parent and build symbolic links to them.

The web interface is available at the following port:

```yaml
navidrome_host_port: 48533
```

### Bonob

If you have e.g. a Sonos system in the house, you may install also Bonob by setting `bonob_enabled` to `true`. the default is:

```yml
bonob_enabled: false
```
You can also specify the bonob image version and the port at which is available:

```yml
bonob_image_version: 'latest'
bonob_host_port: 48534
```

You can change the colors of the bonob icon displayed:

```yml
bonob_icon_color: "beige"
bonob_icon_background: "red"
```
#### Sonos

The sonos-related variables are:

```yml
bonob_sonos_auto_register: 'true'
bonob_sonos_device_discovery: 'true'
bonob_sonos_seed_host: 
bonob_sonos_service_id: "246"
```

If you try sonos autodiscovery and it doesn't work, please:

1. Find the IP of one of the Sonos devices
2. Set `bonob_sonos_seed_host` to that IP
3. Replay the role

You can also add custom clients for streaming:

```yaml
bonob_subsonic_custom_clients: 'audio/flac'
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
    bonob_enabled: "true"
  roles:
    - 'laurivan.navidrome'

```

## License

MIT

## Author Information

This role was created in 2022 by [Laur Ivan](https://www.laurivan.com).
