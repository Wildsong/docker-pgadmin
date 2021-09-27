# docker-pgadmin

I set this instance of pgadmin4 specifically to examine Esri ArcGIS Portal and DataStore tables.
There is nothing special about it except a few usage notes regarding Esri products
in this README.

It's about as a simple as I could make it. It's built on the official image.

I will probably integrate it into the Arctic project eventually.

## Configure

You need to define a username and password, that is done in the .env file.
Copy the sample file and edit it.

```bash
cp sample.env .env
```

Edit .env to set username and password.

## Deploy

Start it up,

```bash
docker-compose up -d
```

then access it on port 8123 via browser. The port is set in the docker-compose.yml file
and I chose 8123 totally arbitrarily.

## Usage

Once you have it up in a browser window, refer to the docs for pgadmin4.

### Portal

If your Portal and your pgadmin are on separate machines you have to add a line to pg_hba.conf
and then restart the Portal. The file on Windows is in C:/arcgis/arcgisportal/db
and the line I added to give my dockerized pgadmin access was


```bash
host  all     arcgis     10.10.10.210/32 scram-sha-256
```

The Portal PostgreSQL instance runs at port 7654.

The column with USER in it needs to have your admin user in it, in this sample it's "arcgis".
The IP address needs to be the one for the machine where pgadmin runs.

Typos in pg_hba.conf will prevent Portal from functioning. Back up before editting.

This copy of PostgreSQL is running on port 

### DataStore

You have to access the DataStore using the "sde" account.

You can find your DataStore password for sde by running listadminusers on the server it's installed on,
for Windows it's in C:/Program Files/ArcGIS/DataStore/tools. (Run as administrator)

The DataStore PostgreSQL instance runs at port 9876.

If your DataStore and your pgadmin are on separate machines you have to add a line to pg_hba.conf
and then restart the Datastore. The file on Windows is in C:/arcgis/arcgisdatastore/pgdata
and then line I added to give my dockerized pgadmin access was.

```bash
host  all     sde     10.10.10.210/32 scram-sha-256
```

This gives access only to the machine living at 10.10.10.210 and requires a password.

After you edit pg_hba.conf you must restart the PostgreSQL server, I do that by restarting ArcGIS Datastore.

Note that if you get this line wrong, your PostgreSQL instance will
not restart, the ArcGIS Datastore will say that it restarted but when
you check the logs it will tell you there is an error in the file.


