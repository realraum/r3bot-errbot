# r3bot-errbot

[errbot](http://errbot.io/) for realraum related chat (IRC, XMPP, Telegram, ...) stuff.


## Configuration

* `mkdir /opt/errbot/r3bot && cd $_`
* `git clone https://github.com/realraum/r3bot-errbot.git .`
* `mkdir ssl data plugins`

And then

* Configuration via environment variables, see `config.py` and `env.list`
* Configuration by adapting `config.py` (and lunching `run.sh` with it)

## Systemd

* Use [systemd-docker](https://github.com/ibuildthecloud/systemd-docker)

```
[Unit]
Description=Errbot r3bot
After=docker.service
Requires=docker.service

[Service]
WorkingDirectory=/opt/errbot/r3bot
ExecStart=/opt/bin/systemd-docker run --rm --name r3bot-errbot -it -v .:/srv --env-file ./env.list -e TZ=Europe/Vienna realraum/r3bot-errbot /app/venv/bin/run.sh -c /srv/config.py
Restart=always
RestartSec=10s
Type=notify
NotifyAccess=all
TimeoutStartSec=120
TimeoutStopSec=15

[Install]
WantedBy=multi-user.target
```


## Plugin development

* [errbot manual](http://errbot.io/en/latest/index.html#user-guide)
* `pip install -r requirements.txt; errbot -T` (in this directory)


## Credits

* Docker stuff based on [rroemhild/docker-errbot](https://github.com/rroemhild/docker-errbot)
* Plugins based on [realraum/r3bot-irc](https://github.com/realraum/r3bot-irc)