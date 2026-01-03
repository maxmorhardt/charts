# External Dependencies

## Required

- **PostgreSQL Database** - Version 12+
- **Redis Cache** - For sessions and caching
- **SMTP Server** - For sending emails
- **Environment Secret** - Name: `squares-api-env`

```bash
kubectl create secret generic squares-api-env \
  --from-literal=db-host='postgres.example.com' \
  --from-literal=db-port='5432' \
  --from-literal=db-user='squares_user' \
  --from-literal=db-password='your-password' \
  --from-literal=db-name='squares' \
  --from-literal=db-ssl-mode='require' \
  --from-literal=redis-host='redis.example.com:6379' \
  --from-literal=smtp-host='smtp.example.com' \
  --from-literal=smtp-port='587' \
  --from-literal=smtp-user='noreply@example.com' \
  --from-literal=smtp-password='your-password' \
  --from-literal=support-email='support@example.com' \
  --from-literal=jwt-secret='your-secret'
```

## Optional

- **NGINX Ingress Controller** - If ingress enabled
- **TLS Secret** - If ingress enabled (name: `maxstash.io-tls`)
- **DNS Record** - Point `api.maxstash.io` to ingress external IP
- **Prometheus** - For metrics collection
