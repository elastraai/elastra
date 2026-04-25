# Elastra

Public landing page for the Elastra on-prem runtime.

The public Docker image is published separately. This repository intentionally does not contain private runtime internals, database schema, bootstrap SQL, or release operations material.

## License

The Elastra Public Runtime Edition is licensed, not sold.

- Proprietary license for internal customer use only
- No redistribution of the Docker image, binaries, or runtime artifacts to third parties
- No use as a hosted SaaS, managed service, MSP, OEM, or white-label platform for third parties
- Full terms: https://help.elastra.ai/on-prem

## Documentation

Full product documentation:

```text
https://help.elastra.ai
```

On-prem guide:

```text
https://help.elastra.ai/on-prem
```

## Docker Compose

Create a local folder for the runtime, download the public compose file from this repository, and start the stack:

```bash
mkdir -p elastra-onprem && cd elastra-onprem
curl -fsSL https://raw.githubusercontent.com/elastraai/elastra/main/docker-compose.yml -o docker-compose.yml
docker compose up -d
```

The web UI is available at:

```text
http://localhost:8080
```

## CLI

Install the Elastra CLI from the public download endpoint:

```bash
curl -fsSL https://api.elastra.ai/v1/downloads/install.sh | bash
```
After the local on-prem runtime is running, point the CLI at the local server and authenticate:

```bash
export ELASTRA_API_URL=http://localhost:8080
elastra auth login
elastra init
```

## On-Prem Runtime

The on-prem runtime is distributed as a public Docker image.

Current image namespace:

```text
ghcr.io/elastraai/elastra
```

## Notes

- `OPENAI_API_KEY` and `ANTHROPIC_API_KEY` are optional for baseline runtime operation.
- The public runtime can operate with its internal embeddings generator.
