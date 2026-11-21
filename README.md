# ISEP Security CTF

A shared repository for security and CTF challenges. Each challenge lives in
its own folder under `challenges/` and includes a description and a separate
file with three progressive hints.

## Challenges

| Challenge | Category | Difficulty | Start |
| --- | --- | --- | --- |
| [Apache Path Traversal](challenges/apache-path-traversal/README.md) | Web | TBD | `docker compose -f challenges/apache-path-traversal/docker-compose.yml up --build` |

Each challenge's hints are in its `hints.md` file. If you want to solve a
challenge without help, read them only when needed.

## Requirements

- [Docker](https://docs.docker.com/get-docker/) with Docker Compose

## Run a challenge locally

Run this from the repository root:

```powershell
docker compose -f challenges/apache-path-traversal/docker-compose.yml up --build
```

The challenge will be available at <http://127.0.0.1:8080>. To stop it, press
`Ctrl+C` in the same terminal, then clean up:

```powershell
docker compose -f challenges/apache-path-traversal/docker-compose.yml down
```

Each challenge may have its own start and stop instructions. Check the
challenge's `README.md`.

## Contributing a challenge

1. Choose a unique, lowercase folder name with hyphens, for example
   `challenges/my-new-topic/`.
2. Copy `README.md` and `hints.md` from
   [`templates/challenge/`](templates/challenge/).
3. Add the challenge files (such as source code, configuration, or container
   files) to the same folder.
4. Add an entry to the challenge table above.
5. Review the checklist in [CONTRIBUTING.md](CONTRIBUTING.md) before opening a
   pull request.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details on folder names, hints, and
the team workflow.

## Safety

Challenges are intentionally vulnerable and are meant only for a local,
authorized learning environment. Do not expose them to the public internet.
Never commit real credentials, personal data, or production secrets; flags
must be synthetic values created specifically for the challenge.
