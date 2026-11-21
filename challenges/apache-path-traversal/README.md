# Apache Path Traversal

| Property | Value |
| --- | --- |
| Category | Web |
| Difficulty | TBD |
| Environment | Docker Compose, Apache |

## Description

An internal archive portal has been migrated to an older Apache version.
Examine the local challenge environment and find out which resource is not
protected as intended.

## Learning objective

Read Apache configurations and understand how URL mappings and filesystem
paths affect resource accessibility.

## Requirements

- Docker with Docker Compose
- A web browser

## Start

Run this from the repository root:

```powershell
docker compose -f challenges/apache-path-traversal/docker-compose.yml up --build
```

## Access and objective

The portal is available locally at <http://127.0.0.1:8080>. The flag is
intended only for the local challenge environment. Do not use real credentials
or data from other systems.

## Stop and cleanup

Press `Ctrl+C` in the terminal running the Compose process, then run this from
the repository root:

```powershell
docker compose -f challenges/apache-path-traversal/docker-compose.yml down
```

## Hints

The three progressive hints are in [`hints.md`](hints.md).
