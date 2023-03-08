# Simple greeting service on Liberty Profile

## Start in dev mode

```bash
./mvnw liberty:dev
```

## Package

```bash
./mvnw clean package
```

## Build an application image

```bash
# Open Liberty
podman build --platform=linux/amd64 -t greeting-ol:latest -f Dockerfile-ol .

# WebSphere Liberty
podman build --platform=linux/amd64 -t greeting-wl:latest -f Dockerfile-wl .
```

## Run a container

```bash
# Open Liberty
export GREETINGS="Hello from Open Liberty.;How are you?"
podman run -d --name greeting-ol --rm -p 9080:9080 -e GREETINGS=$GREETINGS greeting-ol:latest

# WebSphere Liberty
export GREETINGS="Hello from WebSphere Liberty.;How are you?"
podman run -d --name greeting-wl --rm -p 9081:9080 -e GREETINGS=$GREETINGS greeting-wl:latest
```

## Endpoints

The `/greetings` endpoint is accessible at `http://<host>:<port>/api/greetings`

## Environment variables

| Env         | Description                        | Default value                          |
| ----------- | ---------------------------------- | -------------------------------------- |
| `GREETINGS` | A list of greetings divided by ";" | `(You did not specify any greetings.)` |
