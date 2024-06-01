# Docker Compose Project to Install the Lyrion Music Server

* builds a docker container with the Logitech/Music Server

## References

https://lyrion.org/lms-server-repository/

## How to use
* check/adapt the path settings in the .env first
* build the container

```bash
cd lms
sudo docker compose build
```

* start the container

```bash
sudo docker compose up
# or
sudo docker compose up -d
```

* stop the container
```bash
sudo docker compose down
```
* have fun :)
