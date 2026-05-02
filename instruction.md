# Build Instructions

## 1. Encode apps.json to Base64

```bash
export APPS_JSON_BASE64=$(base64 -w 0 apps.json)

echo $APPS_JSON_BASE64
```

## 2. Build Docker Image

```bash
docker buildx build \
  --load \
  --build-arg FRAPPE_BRANCH=version-16 \
  --build-arg APPS_JSON_BASE64=$APPS_JSON_BASE64 \
  --file images/layered/Containerfile \
  --tag {username}/frappe-aio:13feb2026 \
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
