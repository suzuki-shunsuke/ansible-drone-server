# ansible-drone-server

ansible role to install [drone-server](http://docs.drone.io/installation/).

* [suzuki-shunsuke.drone-server](https://galaxy.ansible.com/suzuki-shunsuke/drone-server/)

## Requirements

* Docker Engine
* docker-py

## Role Variables

name | required | default | description
--- | --- | --- | ---
drone_server_env | yes | {} |
drone_server_docker_network_name | no | drone |
drone_server_docker_image_name | no | drone/drone |
drone_server_docker_image_tag | no | latest |
drone_server_port | no | 8000 |
drone_server_grpc_port | no | 9000 |
drone_server_container_name | no | drone-server |
drone_server_volumes | no | ["/var/lib/drone:/var/lib/drone/{}".format(drone_server_env.get('XDG_CACHE_HOME', '/var/lib/drone'))] |
drone_server_network_mode | no | null |

About `drone_server_env`, see the following links.

* http://docs.drone.io/installation/
* https://github.com/drone/drone/blob/master/cmd/drone-server/server.go

## Dependencies

Nothing.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: suzuki-shunsuke.drone-server
      drone_server_docker_image_tag: 0.8.2
      drone_server_env:
        DRONE_OPEN: "true"
        DRONE_ORGS: suzuki-shunsuke
        DRONE_ADMIN: suzuki-shunsuke
        DRONE_HOST: "https://drone.example.com"
        DRONE_GITHUB: "true"
        DRONE_GITHUB_CLIENT: "drone_github_client"
        DRONE_GITHUB_SECRET: "drone_github_secret"
        DRONE_SECRET: "drone-secret"
        DRONE_DATABASE_DRIVER: mysql
        DRONE_DATABASE_DATASOURCE: drone:password@tcp(127.0.0.1:3306)/drone?parseTime=true
        GIN_MODE: release
      become: yes
```

## Change Log

See [CHANGELOG.md](CHANGELOG.md).

## See also

* [suzuki-shunsuke.drone-agent](https://github.com/suzuki-shunsuke/ansible-drone-agent): ansible role to install drone-agent

## License

[MIT](LICENSE)
