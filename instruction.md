# Build Instructions

## Build Docker Image

> **Security Note:** `apps.json` is passed via BuildKit `--secret` instead of `--build-arg` to prevent
> sensitive data (private repo URLs/tokens) from being persisted in image metadata.

```bash
docker buildx build \
  --load \
  --no-cache \
  --build-arg FRAPPE_BRANCH=version-16 \
  --secret id=apps_json,src=apps.json \
  --file images/layered/Containerfile \
  --tag achelesstech/frappe-aio:latest \
  .
```

## apps.json

```json
[
    {
      "url": "https://github.com/frappe/erpnext",
      "branch": "version-16"
    },
    {
      "url": "https://github.com/frappe/payments",
      "branch": "version-16"
    },
    {
      "url": "https://github.com/frappe/hrms",
      "branch": "version-16"
    },
    {
      "url": "https://github.com/frappe/crm",
      "branch": "main"
    },
    {
      "url": "https://github.com/frappe/lms",
      "branch": "main"
    }
]
```
