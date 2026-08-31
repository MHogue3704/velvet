# Deploy Velvet with Dockhand

Velvet is packaged as a standard Docker Compose stack. It builds the app from
this directory and publishes it on port `3088` by default.

## Add the API key in `.env`

Open `.env` in the same directory as `compose.yaml` and set:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

Do not commit `.env`; it is already excluded from Git and from the Docker image.
The committed `.env.example` file is a safe template without credentials.

## From a Git repository

1. Push this folder to a Git repository that Dockhand can access.
2. In Dockhand, open **Stacks** and choose **From Git**.
3. Select the repository and branch.
4. Set **Compose file path** to `compose.yaml`.
5. Leave the context directory at the repository root, or set it to the folder
   containing this file when Velvet is inside a larger repository.
6. Enable **Build images on deploy**.
7. Add the environment variables below in Dockhand, or place a private `.env`
   beside `compose.yaml`, then deploy the stack.

## Environment variables

| Variable | Required | Purpose |
| --- | --- | --- |
| `OPENAI_API_KEY` | For live AI | Server-side OpenAI API key. Keep it in Dockhand's environment editor, never in Git. |
| `OPENAI_MODEL` | No | Defaults to `gpt-5-mini`. |
| `VELVET_PORT` | No | Host port; defaults to `3088`. |
| `SITE_URL` | Recommended | Public URL used for page and social metadata, such as `https://velvet.example.com`. |

Without `OPENAI_API_KEY`, Velvet remains usable with its built-in demo replies.

## Local verification

```sh
docker compose up --build -d
docker compose ps
```

Open `http://localhost:3088`. To stop it, run `docker compose down`.
