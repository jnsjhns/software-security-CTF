# Contributing to the CTF Repository

Follow these conventions to keep challenges consistent and easy to run
locally.

## Folder structure

Each challenge gets its own folder directly under `challenges/`:

```text
challenges/
  unique-challenge-slug/
    README.md
    hints.md
    # Challenge files, for example src/, Dockerfile, or docker-compose.yml
templates/
  challenge/
    README.md
    hints.md
```

- Slugs must be unique and descriptive, and use lowercase letters, numbers,
  and hyphens.
- Keep each challenge self-contained. Its files and startup configuration
  belong in its challenge folder.
- Keep templates in `templates/challenge/`, not in `challenges/`, so they
  aren't mistaken for playable challenges.
- If the number of challenges grows substantially, the folders can later be
  grouped by category. Until then, keep them directly under `challenges/`.

## Documentation

Each challenge must have a `README.md` with at least:

- Name, category, and difficulty (or "TBD")
- A short description and learning objective that don't reveal the solution
- Requirements and tested environment
- Start, access, and stop instructions
- Flag format or submission instructions, if relevant

Each challenge must also have a `hints.md` with exactly three numbered hints.
They should progress from general to specific:

1. A prompt or relevant observation
2. Narrow down the area or concept
3. A concrete approach, but not the finished flag

Hints should be helpful without unnecessarily revealing the full solution or
challenge secrets.

## Team workflow

1. Before creating a challenge, check whether a similar one or matching slug
   already exists.
2. Work on a dedicated branch and copy the templates.
3. Test the challenge locally and follow the instructions in its README.
4. Update the challenge index in the root `README.md`.
5. Open a pull request with a short description, category, and test results.
   Ask another team member to review the documentation and verify that it runs.

## Safety and quality checklist

- [ ] The challenge runs only in its intended local/test environment.
- [ ] Container ports are bound to `127.0.0.1` where possible.
- [ ] No real secrets, private data, or production credentials are committed.
- [ ] Flags are synthetic test values created for the challenge, not reused
      credentials.
- [ ] The `README.md` has complete start and stop instructions.
- [ ] The `hints.md` has exactly three progressive hints and no finished flag.
- [ ] The challenge index in the root `README.md` is up to date.
