# Primer prompt: desplegar Kweekly CRM en Railway

Texto listo para copiar en un nuevo trabajo abierto sobre este repositorio. Objetivo de esta etapa: desplegar y verificar una instancia piloto del fork; la revisión Tech Provider pertenece a etapas posteriores.

---

Trabaja en /Users/jehusilva/kinetia-products/kweekly-crm, fork de Vocero CRM renombrado como Kweekly CRM. Lee AGENTS.md, README.md, CLAUDE.md, docs/kweekly/plan-general.md y docs/kweekly/procedencia.md. Aplica use-railway; consulta la documentación oficial vigente para decisiones de infraestructura. Conserva LICENSE y atribución upstream.

Quiero que prepares, despliegues y verifiques una instancia piloto de Kweekly CRM en mi Railway. El objetivo es obtener una base estable para validar el CRM y después avanzar hacia Meta Tech Provider. No implementes todavía Embedded Signup ni envíes App Review.

1. Revisa el estado Git, Dockerfile, entrypoint, pnpm-lock.yaml, migraciones, env.ts y healthcheck. Preserva cambios existentes. Construye este fork; no uses la imagen preconstruida del upstream como si incluyera la marca Kweekly. Reproduce la compilación con la versión compatible de Node y pnpm fijado.
2. Identifica la cuenta, workspace, proyecto, ambiente y servicio de Railway. Inspecciona recursos existentes antes de crear otros. Usa un ambiente piloto aislado y PostgreSQL dedicado; evita modificar el Kweekly anterior. Si hay varias ubicaciones igualmente plausibles, solicita una sola aclaración concreta antes de la mutación dependiente. Esta solicitud autoriza el despliegue del piloto, no una migración o reemplazo del producto actual.
3. Prepara el servicio CRM con su Dockerfile, referencia privada a DATABASE_URL, volumen en /data, MEDIA_DIR=/data/media, puerto coherente con PORT/3000, HOSTNAME=0.0.0.0 y healthcheck /api/health. Examina el arranque de migraciones y los permisos del volumen. No añadas Coolify ni Caddy a Railway.
4. Configura URL HTTPS y secretos mediante Railway, sin mostrarlos ni guardarlos en Git. Genera secretos nuevos para este piloto y conserva ENCRYPTION_KEY de manera segura. Si falta acceso a un secreto necesario, explica dónde introducirlo sin pedir pegarlo en el chat. Mantén IA, canales secundarios, atribución y agenda apagados en la primera validación. Determina cómo crear el administrador inicial y cerrar el registro público.
5. Despliega y verifica SUCCESS del despliegue específico. Comprueba HTTPS, salud, acceso, marca Kweekly CRM, creación/lectura de datos, subida/lectura de archivo, persistencia después de un reinicio y funcionamiento básico de SSE. Un 200 o un upload concluido no bastan. No reportes como validado lo que no puedas probar.
6. Configura una estrategia de respaldo de PostgreSQL y medios con retención definida y prueba de restauración aislada. Documenta reversión de imagen y compatibilidad de esquema; no borres volúmenes ni bases para resolver un error.
7. No conectes todavía WABA/números reales, no cambies callbacks de Meta existentes y no envíes mensajes a terceros. Esa validación se realizará en una etapa explícita con activos de prueba y destinatarios autorizados. No leas ni copies secretos del Kweekly anterior.
8. Corrige fallos de build, arranque o permisos necesarios para este piloto. Ejecuta typecheck, lint, tests pertinentes y build; añade pruebas solo para cambios de comportamiento que lo justifiquen. Mantén un registro de evidencias, pendientes y limitaciones sin datos sensibles.

Entrega la URL del piloto si quedó desplegado, el estado verificado, recursos utilizados, cambios realizados, comprobaciones y sus resultados, un runbook reproducible y el próximo paso para validar WhatsApp. Si existe un bloqueo real, completa primero el trabajo independiente y explica exactamente qué dato o acceso falta. No afirmes aprobación de Meta ni disponibilidad comercial por terminar el despliegue.
