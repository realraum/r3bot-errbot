# r3bot-errbot

[errbot](http://errbot.io/) for realraum related chat (IRC, XMPP, Telegram, ...) stuff.


## Configuration

* Configuration via environment variables, see `config.py`.
* Configuration by adapting `config.py` (and lunching `run.sh` with it)


## Systemd

* Use [systemd-docker](https://github.com/ibuildthecloud/systemd-docker)

```
[Unit]
Description=Errbot LosFuzzys
After=docker.service
Requires=docker.service

[Service]
ExecStart=/opt/bin/systemd-docker run --rm --name r3bot-errbot -it -v /opt/errbot/r3bot:/srv -e TZ=Europe/Vienna realraum/r3bot-errbot /app/venv/bin/run.sh -c /srv/config.py
Restart=always
RestartSec=10s
Type=notify
NotifyAccess=all
TimeoutStartSec=120
TimeoutStopSec=15

[Install]
WantedBy=multi-user.target
```


## Credits

* Docker stuff based on [rroemhild/docker-errbot](https://github.com/rroemhild/docker-errbot)
* Plugins based on [realraum/r3bot-irc](https://github.com/realraum/r3bot-irc)