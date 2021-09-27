# docker-pgadmin

This freestanding instance of pgadmin4 is used
to examine ArcGIS Datastore tables right now.

It's about as a simple as I could make it. It's built on the official image.

## Configure

```bash
cp sample.env .env
```

Edit .env to set username and password.

## Deploy

Start it up,

```bash
docker-compose up -d
```

then access it on port 8123. The port is set in the docker-compose.yml file.

# Use

Once you have it up in a browser window, refer to the docs for pgadmin4.



