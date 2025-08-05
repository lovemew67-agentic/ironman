# infra

## host (mac mini intel 2018)

- done: nomachine (4000)
- done: cloudflare tunnel
	- broswer ssh rendering

## cluster (mac mini intel 2018)

- done: docker desktop
	- tmux + nohup + socat
	- ```
	  nohup socat TCP-LISTEN:2375,reuseaddr,fork,bind=192.168.2.131 UNIX-CLIENT:/var/run/docker.sock &
	  ```
	- ```
	  DOCKER_HOST=tcp://192.168.2.131:2375 docker images
	  ```
	- ```
	  ssh -L 0.0.0.0:2375:192.168.2.131:2375 -L 0.0.0.0:2322:192.168.2.131:22 -L 0.0.0.0:6443:192.168.2.131:6443 -L 0.0.0.0:30443:192.168.2.131:30443 -o StrictHostKeyChecking=no -o GlobalKnownHostsFile=/dev/null -o UserKnownHostsFile=/dev/null -p 22 root@remote.ip
	  ```
- done: docker compose
	- loki (3100)
	- tempo (4317)
	- mimir (9090)
	- pyroscope (4040)
	- grafana (3000)
	- node-exporter (9100)
	- cadvisor (8080)
- done: kind
    - ```
	  DOCKER_HOST=tcp://127.0.0.1:2375 kind create cluster --name ironman --kubeconfig ./kubeconfig --config kind.yaml
	  ```
    - ```
	  DOCKER_HOST=tcp://127.0.0.1:2375 kind delete cluster --name ironman --kubeconfig ./kubeconfig
	  ```

## worker (mac mini intel 2018)

- wip:  android studio
- wip:  github runner
- wip:  xcode
