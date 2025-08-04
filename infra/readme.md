# infra

## host (mac mini intel 2018)

- done: nomachine (4000)
- done: cloudflare tunnel
	- broswer ssh rendering

## cluster (mac mini intel 2018)

- done: docker desktop
	- tmux + nohup + socat
	- nohup socat TCP-LISTEN:2375,reuseaddr,fork,bind=192.168.2.131 UNIX-CLIENT:/var/run/docker.sock &
	- DOCKER_HOST=tcp://192.168.2.131:2375 docker images
- done:  docker compose
	- loki (3100)
	- tempo (4317)
	- mimir (9000)
	- pyroscope (4040)
	- grafana (3000)
	- node-exporter (9100)
	- cadvisor (8080)
- wip:  kind

## worker (mac mini intel 2018)

- wip:  android studio
- wip:  github runner
- wip:  xcode
