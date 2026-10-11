---
title: n8n en español
emoji: 🔀
colorFrom: red
colorTo: gray
sdk: docker
app_port: 7860
pinned: false
---

# n8n en español (Hugging Face Space)

Este Space ejecuta n8n 2.43.3 con la interfaz traducida al español rioplatense.
Usa la imagen oficial `n8nio/n8n:2.43.3` y reemplaza solo el frontend.

## Crear el Space

1. Entrá a https://huggingface.co/new-space.
2. Elegí **Docker** como SDK y la plantilla **Blank**.
3. Elegí el hardware gratis (**CPU basic**).
4. Subí este `README.md` y el `Dockerfile` a la raíz del Space.

## Secretos obligatorios

Definilos en **Settings → Variables and secrets** del Space, como **Secrets**:

| Secreto | Valor |
| --- | --- |
| `N8N_ENCRYPTION_KEY` | Un texto aleatorio largo. No lo cambies nunca: cifra tus credenciales. |

## Persistencia (muy recomendado)

El disco del Space se borra cada vez que se reinicia o se reconstruye.
Sin una base de datos externa, perdés workflows, credenciales y usuarios.

Usá un Postgres gratis (por ejemplo Supabase o Neon) y agregá estos secretos:

| Secreto | Ejemplo |
| --- | --- |
| `DB_TYPE` | `postgresdb` |
| `DB_POSTGRESDB_HOST` | `db.xxxxx.supabase.co` |
| `DB_POSTGRESDB_PORT` | `5432` |
| `DB_POSTGRESDB_DATABASE` | `postgres` |
| `DB_POSTGRESDB_USER` | `postgres` |
| `DB_POSTGRESDB_PASSWORD` | la contraseña de tu base |
| `DB_POSTGRESDB_SSL_ENABLED` | `true` |

## Uso

- Abrí el Space con su URL directa: `https://<usuario>-<space>.hf.space`.
  Dentro del iframe de huggingface.co el inicio de sesión puede fallar por las cookies.
- La primera vez, n8n te pide crear la cuenta de propietario.
- La URL de webhooks se toma sola de `SPACE_HOST`.

## Límites del plan gratis

- El Space se duerme después de 48 horas sin visitas. Dormido, no ejecuta triggers ni webhooks.
- Al despertar tarda un par de minutos en arrancar.
- Si el Space es público, cualquiera puede ver la pantalla de login. Usá una contraseña fuerte.
  Un Space privado protege el acceso, pero los webhooks externos no van a poder llamarlo.
