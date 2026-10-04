# Kweekly CRM

Un producto de Kinetia. Base de desarrollo derivada de [Vocero CRM](https://github.com/kevinrivm/vocero-crm), con licencia MIT conservada.

## Estado

Fork creado y código instalado localmente. Nombre inicial **Kweekly CRM** y acento **#0057FF**, usando el mecanismo de marca existente. No desplegado en Railway ni aprobado como Tech Provider. Las configuraciones de marca por negocio conservan prioridad. La inicial generada por el sistema es provisional; no es un nuevo logotipo aprobado.

Una instancia = un negocio. La presencia de organization_id no acredita por sí sola un SaaS con onboarding multiempresa. Embedded Signup requiere desarrollo y revisión propios. La aprobación de Vocero Cloud no se transfiere a este fork.

## Empieza aquí

- [Plan general: Railway y Meta](docs/kweekly/plan-general.md)
- [Primer prompt: despliegue piloto en Railway](docs/kweekly/prompt-despliegue-railway.md)
- [Procedencia y alcance del cambio](docs/kweekly/procedencia.md)
- [Documentación original de Vocero](README.upstream.md)
- [Variables sin secretos](.env.example)

## Desarrollo

Node compatible con package.json y pnpm fijado por packageManager. Instalar con pnpm install --frozen-lockfile. Typecheck, lint, test y build son los controles heredados. El arranque necesita PostgreSQL y variables locales válidas; la instalación de dependencias no equivale a una instancia funcionando.

Para Railway, construir **este fork desde su Dockerfile**, con PostgreSQL dedicado y volumen en /data. Las recetas heredadas de Coolify/Compose que usan ghcr.io/kevinrivm/vocero-crm ejecutan la imagen de Vocero original, no la marca de este fork. Ver el plan antes de desplegar.

Conservar LICENSE y atribución al redistribuir. No cambiar credenciales, activos de WhatsApp ni datos del Kweekly existente como consecuencia de este fork.
