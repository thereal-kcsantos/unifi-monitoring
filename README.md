# unifi-monitoring
Tools to monitor Unifi Networks.

Featuring Unpoller, Grafana, and InfluxDB. Installed via Docker (Docker Compose). At the time of writing this, this was built on a macOS environment. YMMV if you decide to use install this on a Linux machine

**Required services:**
Docker (if Mac, Docker Desktop)
docker compose
git
Github CLI tools

## Environment setup

**Requirements:**
- Docker (if Mac, Docker Desktop)
- docker compose
- git
- Github CLI tools

### Host Directoriess
Here's a view of the file structure that I've decided to use:

```
(~/docker/)
/Users/$CURRENTUSER/docker
├── grafana
├── influxdb
└── unifi-monitoring
    ├── README.md
    └── unpoller
        ├── docker-compose-unpoller.yaml
        ├── example-unpoller.env
        └── unifi-poller.conf
```

Let's start by adding all the folders and files to use.

1. Create `~/docker/` folder to store all of our docker config files
2. Create the `~/docker/grafana/` folder
    - This will be used for the Grafana volume
3.  Create the `~/docker/influxdb/` folder
    - This will be used for the InfluxDB volume
4. Switch to the ~/docker/ directory and add this repo
```
mkdir ~/docker
mkdir ~/docker/grafana
mkdir ~/docker/influxdb
cd ~/docker/
gh repo clone thereal-kcsantos/unifi-monitoring

```
### Environment variables file
5. Create the `.env` file in the ~/Users/$CURRENTUSER/docker/unifi-monitoring/unpoller/ directory, copied from the `example-unpoller.env` example file.
_the .env is the environment file for Docker Compose. At the time of writing this, defining the `env_file` via Docker Compose does not work (at least it didn't for me). To make it easier, we will use the default Environments file name, using  `.env`_
- The `.env` file needs to be in the same directory as the docker-compose.yaml file (docker-compose-unpoller.yaml
```
cp ~/docker/unifi-monitoring/unpoller/example-unpoller.env ~/docker/unifi-monitoring/unpoller/.env
```

6. Edit the `.env` file to fit your needs. The following variables need to be changed:
    
- `UP_UNIFI_DEFAULT_USER`
- `UP_UNIFI_DEFAULT_PASS`
- `UP_UNIFI_DEFAULT_URL`

### Unifi Poller Configuration File
7. Create the `unifi-poller.conf` file in the ~/Users/$CURRENTUSER/docker/unifi-monitoring/unpoller/ directory, copied from the `example-unifi-poller.conf` example file.

- Keep the `unifi-poller.conf` file in the same directory as the docker-compose.yaml file (docker-compose-unpoller.yaml)

```
cp ~/docker/unifi-monitoring/unpoller/example-unifi-poller.conf ~/docker/unifi-monitoring/un
poller/unifi-poller.conf
```

8. Edit the `unifi-poller.conf` file variables:
- `[unifi.defaults] > url` enter the URL of your unifi controller. If this is a Unifi Dream Gateway (Unifi Dream Machine line, or any other unifi router with a built in controller) OR a Unifi Cloud Key, just the address is fine, i suggest removing the Port number.
    - IF this is a Self Hosted controller, you should add the port number at the end of the address.
     - Example:
       ```
       [unifi.defaults]
       url  = "https://192.168.1.10:8443"
       ```
-  `[unifi.defaults] > user` enter the read-only username you created in your unifi controller
-  `[unifi.defaults] > password` enter the password for the read-only user you created in your unifi controller
-  `[influxdb] > url` enter the influxdb address with the 8086 port number.
    ```
    [influxdb]
    url  = "http://127.0.0.1:8086"
    ```


## Start Docker Containers

9. Start the Docker containers in detached mode (-d)

```
docker compose -f ~/docker/unifi-monitoring/unpoller/docker-compose-unpoller.yaml up -d
```

## Grafana Setup

10. Sign into the Grafana Console:

`http://Address-of-Host:8086`

The default username and password is `admin`/`admin`

11. Setup InfluxDB Data Source

`Menu` > `Connections` > `Add new connection` > search `InfluxDB` > `Add new data source`
- **HTTP** 
    - `URL`: http://Address-of-Host:8086 (http://192.168.1.10:8086, http://address-of-host.local:8086, etc.)
    - `Allowed cookies`: server
- **InfluxDB Details**
    - `Database`: unifi (this should match your "INFLUXDB_DB" variable in your .env file)
    - `User`: unifi (this should match your "INFLUXDB_ADMIN_USER" variable in your .env file)
    - `Password`: unifi (this should match your "INFLUXDB_ADMIN_PASSWORD=unifi
" variable in your .env file)
    - Everything else can be left at default/blank
- Click `Save & test`
    * **_If successful, you will get a message along the lines of "datasource is working. 12 measurements found"_**








