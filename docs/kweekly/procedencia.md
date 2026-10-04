# Procedencia de Kweekly CRM

- Origen: https://github.com/kevinrivm/vocero-crm
- Fork: https://github.com/JehuSilva/kweekly-crm
- Commit de origen: 831e65ecc6b0d5b46a1c32556956df57244fd185
- Versión declarada upstream: 1.4.0. El commit fija la base exacta; no implica identidad con el tag 1.4.0.
- Licencia: MIT; LICENSE conservado sin cambios.
- Ajuste de contraste: pisos de visibilidad para selección en tema oscuro tras adoptar el azul Kweekly; pruebas existentes mantienen su exigencia.
- Cambios iniciales: nombre del paquete, marca por defecto, preset azul Kweekly, textos visibles puntuales, firma de producto en acceso y documentación de implementación.
- Conservado: esquemas/migraciones, rutas, nombres internos y claves de almacenamiento, usuario Linux del contenedor, imágenes y documentación histórica upstream, configuración de agentes.
- Imagen actual: define MEDIA_DIR=/data/media y usa entrypoint para permisos del volumen. Esto resuelve la incertidumbre de la revisión web previa; sigue pendiente comprobarlo en Railway.
- Sin despliegue, migración de datos ni modificación del panel de Meta en esta etapa.

La copia README.upstream.md conserva el documento original. El workflow de imagen usa github.repository para su destino; no crear tags de publicación hasta definir releases propios. Los archivos heredados pueden seguir mencionando Vocero para documentar su origen.
