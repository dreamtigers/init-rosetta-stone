# init system rosetta stone

The following table works as a Rosetta Stone to manage services depending on the
init system[^1] present in your distribution.

Substitute `$service` for the **name of the service** you want to manipulate.

|                         | SysV init[^2]                       | runit                                 | systemd                      |
| ---                     | ---                                 | ---                                   | ---                          |
| List available services | `ls /etc/init.d/`                   | `ls /etc/sv`                          | `systemctl list-unit-files`  |
| List running services   | `service --status-all`              | `ls /var/service`                     | `systemctl list-units`       |
| Start service           | `service $service start`[^3]        | `sv up $service`                      | `systemctl start $service`   |
| Stop service            | `service $service stop`[^3]         | `sv down $service`                    | `systemctl stop $service`    |
| Restart service         | `service $service restart`[^3]      | `sv restart $service`                 | `systemctl restart $service` |
| Get status of service   | `service $service status`[^3]       | `sv status $service`                  | `systemctl status $service`  |
| Enable service          | `update-rc.d $service defaults`[^4] | `ln -s /etc/sv/$service /var/service` | `systemctl enable $service`  |
| Disable service         | `update-rc.d $service remove`[^4]   | `rm /var/service/$service`            | `systemctl disable $service` |

Please consider using a GNU/Linux distribution that does not use `systemd`, like
[Devuan](https://www.devuan.org/) or [Void Linux](https://voidlinux.org/). Read
why: [init freedom](https://www.devuan.org/os/init-freedom).

[^1]: There are a lot of other init systems, but here are the ones I've used.

[^2]: OpenRC builds upon SysV init, so what works for SysV init almost always
  works for OpenRC. Alpine Linux has a quick-start guide for OpenRC,
  [here](https://wiki.alpinelinux.org/wiki/Alpine_Linux_Init_System).

[^3]: Or manually, with: `/etc/init.d/$service {start|stop|restart|status}`.

[^4]: If you don't have `update-rc.d` you have to manually add/remove the
  symlinks to the service, search the internet for a deeper explanation.
