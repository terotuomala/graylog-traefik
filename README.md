# Graylog-Traefik
Graylog stack running in Docker with Traefik as Reverse Proxy. Traefik handles traffic to Graylog Web Interface and Graylog only exposes TCP/UDP ports 514 (Syslog) and 12201 (GELF) for receiving messages.

### Usage with docker-compose
Create docker network for traefik:
```
docker network create traefik-network
```
Start the environment:
```
docker-compose up
```
Open Graylog Web interface using Chrome (because it resolves any *.localhost to the loopback interface): 
```
http://graylog.localhost/
```
Graylog uses initial username `admin` and password `admin`

### Example message
Enable Input e.g. GELF HTTP :
```
System -> Inputs -> Select Input -> GELF HTTP -> Launch new input -> Save
```
Send GELF message via HTTP using curl:
```
curl -X POST -H 'Content-Type: application/json' -d '{ "version": "1.1", "host": "example.org", "short_message": "A short message", "level": 5, "_some_info": "foo" }' 'http://localhost:12201/gelf'
```