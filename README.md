# Hands-On L3: Containers with Docker

ITCS 6190/8190 — Cloud Computing for Data Analysis — Fall 2026

Install Docker Desktop, run a PostgreSQL container, then build and run a Flask web
application with a Redis cache using Docker Compose.

**Worth 1 point.** Submit the link to your own repository on Canvas by 11:59 pm on the day
of the class. Expect 60 to 75 minutes. Work individually.

## The handout

`Hands-On-L3.pdf` in this repository has the full instructions. Read it first.

## Reference files

`starter/` holds correct, working versions of the four files you build in Section 3:

| File | Purpose |
| ---- | ------- |
| `app.py` | Flask application with the Redis hit counter |
| `requirements.txt` | Pinned Python dependencies |
| `Dockerfile` | Builds the web service image |
| `compose.yaml` | Defines the `web` and `redis` services |
| `.gitignore` | Keeps `__pycache__` out of your repository |

Type them out yourself if you want the practice. If you copy them, copy from these files
rather than from the PDF, because indentation does not survive copying out of a PDF and
Python will not run without it.

To run:

```bash
cd starter
docker compose up --build
```

Then open <http://localhost:8000> and refresh a few times. The counter increases because
Redis is holding the count. Press Ctrl+C to stop, then:

```bash
docker compose down
```

## What you submit

Create your **repository public**, and put in it:

- `app.py`, `Dockerfile`, `compose.yaml`, `requirements.txt`
- `README.md` with your execution steps and what you learned, using fenced code blocks
- A document containing screenshots of Docker Desktop showing the running containers, and
  of the application output in the browser
- A `.gitignore`

Then open **one issue per distinct error** you hit. Each issue needs a title naming the
error, a description covering what you expected, what actually happened and the exact
message, the `bug` label, and an assignment to yourself. Say what fixed it, then close it.

Finally, submit your repository link on Canvas.

## Common problems

- **Port 5432 already in use** when starting PostgreSQL: you probably have PostgreSQL
  installed locally. Publish a different host port, for example `-p 5433:5432`.
- **Port 8000 already in use**: change the left-hand side of the mapping in
  `compose.yaml`, for example `"8001:5000"`.
- **`docker: command not found`**: Docker Desktop is not running, or your shell was opened
  before installation finished. Start Docker Desktop and open a new terminal.
- **The web service starts before Redis is ready**: `app.py` retries five times, so give it
  a few seconds. `depends_on` controls start order, not readiness.

## Further reading

- Docker CLI cheat sheet: <https://docs.docker.com/get-started/docker_cheatsheet.pdf>
- Writing and formatting on GitHub:
  <https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax>
