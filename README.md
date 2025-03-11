# QGIS Server example

This repository provides a minimal example of running QGIS Server using the
[official container image](https://github.com/qgis/qgis-docker/blob/main/server/README.md).

Everything boils down to:

- An [example QGIS project and data](./data/example_project)
- A [compose file](./compose.yml) for running the server container

## Running the server

Aside from having docker / podman, there should be no necessary setup.

Start the server with

```
docker compose up -d
```

QGIS server will be available on localhost:8080. For example, to access the WMS
of the example project:

```
localhost:8080/ogc/example_project?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetCapabilities
```

In addition to the basic WMS, the example project defines a print layout with a
map atlas. You can request parts of the atlas with `GetPrint`, `TEMPLATE` and
`ATLAS_PK`, like so:

```
http://localhost:8080/ogc/example_project?SERVICE=WMS
&VERSION=1.3.0
&REQUEST=GetPrint
&FORMAT=pdf
&TEMPLATE=country_atlas
&CRS=EPSG:4326
&ATLAS_PK=1,2
```

Feel free to poke around the example project or make your own. Adding a project
works by adding a directory in [./data](./data), and within that directory
adding the project. Use the `.qgs` format & name the project with the same name
as the parent directory for everything to work automatically.
