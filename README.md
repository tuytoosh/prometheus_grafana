## Run Prometheus + Grafana with Docker Compose

### External network

In order to test it locally I have set up an external netowrk for enable other services to see this service in their networks. So we need to create network manually before next steps:

```
docker netowrk create monitoring
```
### Prometheus configuration

Then modify `prometheus.yml` file and add your services:

```
- job_name: Laravel
    metrics_path: /prometheus
    static_configs:
      - targets: ['laravel.test']
```

My Laravel project is exposing prometheus metrics in the `/prometheus` endpoint and the dns name in `monitoring` network is `laravel.test`.

Finally run the docker compose file with 

```
docker compose up -d
```

### Grafana panel setupC

now you can see the Grafana panel at `http://localhost:3000`. 
Uhttp://prometheus:8080 `admin` for both username and password and add the datasource with this address: `http://prometheus:9090`.

<sub>This text is written in just a few minuts so consider this note as a draft :)</sub>