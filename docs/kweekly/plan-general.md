# Kweekly CRM: del piloto en Railway a Tech Provider

Un producto de Kinetia. Plan de ejecución por etapas para Jehu/Kinetia. Estado inicial: fork y cambio de nombre local; instancia y aprobación pendientes. La primera etapa de trabajo es el despliegue en Railway.

## Objetivo y límites

Construir una experiencia de ventas por WhatsApp sobre Vocero, validarla en infraestructura propia y preparar el onboarding de clientes con sus activos de Meta. Mantener el Kweekly existente como referencia y producto independiente hasta una decisión de evolución basada en evidencia.

Una instancia piloto corresponde a un negocio. No activar altas públicas ni prometer SaaS multiempresa por la presencia de organization_id. Primero demostrar operación, después decidir entre instancias por cliente y un producto realmente multiempresa. Un modelo de instancias por cliente necesita igualmente un mecanismo central de onboarding y administración de conexiones si operamos como Tech Provider.

No se hereda la aprobación de Vocero Cloud. Business Verification, Access Verification, App Review/acceso avanzado y la configuración del onboarding son hitos distintos. Tampoco comprar un servidor concede ninguno de ellos.

## Punto de partida comprobado

- Fork propio y copia en kinetia-products/kweekly-crm, separados de kweekly.
- Upstream fijado por commit en procedencia.md; licencia MIT intacta.
- Base incluye Dockerfile, PostgreSQL/Drizzle, sesiones, credenciales cifradas, bandeja, plantillas, agente opcional, API de cerebro externo y simulación de Laboratorio.
- La imagen actual monta medios en /data/media y ajusta permisos mediante entrypoint. Migraciones al arranque: comprobar el comportamiento real antes de cargar datos.
- Embedded Signup no viene implementado en esta base. El Laboratorio no envía mensajes reales y no constituye evidencia de entrega para Meta.
- En la revisión anterior de Brave: negocio Kinetia verificado; app Kinetia Agency en desarrollo; revisión detallada no enviada; configuración de Login for Business pendiente. Revalidar el panel antes de cambiarlo. No inferir aprobación del resumen que mostraba “en revisión”.
- Existe una WABA propia y conexión del Kweekly anterior. Su callback no debe sustituirse para probar el nuevo CRM sin un análisis de impacto.

## Etapas y criterios de salida

| Etapa | Entregable | Criterio para avanzar | Responsable |
|---|---|---|---|
| 1. Preparar Railway | Configuración reproducible del fork, matriz de variables y runbook | Build, puertos, migraciones y volumen revisados; proyecto/ambiente exactos identificados | Desarrollo |
| 2. Desplegar piloto | Servicio CRM, PostgreSQL y volumen dedicados; HTTPS | Deployment SUCCESS, salud pública, acceso, escritura y persistencia comprobados | Desarrollo + titular de Railway |
| 3. Validar WhatsApp | Espacio de pruebas con activos autorizados | Mensaje entrante, respuesta recibida, plantilla creada/listada y estados reales | Desarrollo + administrador Meta |
| 4. Cerrar cumplimiento | Documentos y callbacks coherentes con el producto | Privacidad/retención comprobables; firma, revocación y eliminación verificadas | Kinetia + desarrollo |
| 5. Construir onboarding | Registro integrado y backend de conexión | Activos vinculados correctamente; pruebas de aislamiento/reconexión y observación en vivo | Desarrollo |
| 6. Preparar revisión | Acceso de revisor, textos por permiso y dos videos | Un revisor puede reproducir el recorrido y cada permiso tiene evidencia específica | Kinetia |
| 7. Completar trámites Meta | Access Verification y App Review según el panel | Resolución y acceso avanzado confirmados por Meta, no solo solicitud enviada | Titular de la app + Meta |
| 8. Piloto externo | Un negocio autorizado conectado con sus activos | Conexión, consentimiento, mensajes y desconexión completos; costos y soporte acordados | Kinetia + negocio piloto |
| 9. Evolucionar Kweekly | Decisión de arquitectura y roadmap de integración | Resultados del piloto y plan de migración/reversión documentados | Kinetia |

## 1–2. Despliegue en Railway: primer bloque

1. Confirmar workspace, proyecto, ambiente y servicio. Reutilizar una ubicación apropiada si existe; evitar duplicar recursos o alterar el Kweekly actual. Registrar la elección sin secretos.
2. Construir desde el Dockerfile del fork. No usar la imagen original de Vocero como si contuviera Kweekly CRM. Conservar pnpm-lock.yaml y la versión del gestor. Docker usa Node 22; comprobar ese entorno además de cualquier comprobación local.
3. Provisionar PostgreSQL dedicado. Referenciar su DATABASE_URL por la red privada. No reutilizar datos o usuarios del producto anterior. Coordinar migraciones al arranque y el arranque de la BD; definir cómo recuperar un despliegue con migración fallida.
4. Montar volumen persistente en /data. MEDIA_DIR=/data/media. Verificar escritura por el usuario real de la imagen, archivos tras reinicio y rutas sin acceso cruzado. No confiar en el filesystem efímero del contenedor.
5. Configurar APP_BASE_URL, DATABASE_URL, BETTER_AUTH_SECRET, ENCRYPTION_KEY, META_WEBHOOK_VERIFY_TOKEN y META_APP_SECRET por el administrador de secretos. No imprimir valores ni copiarlos al repo. La clave de cifrado necesita respaldo seguro: perderla impide descifrar credenciales existentes.
6. Empezar sin proveedor de IA, canales secundarios, atribución ni agenda. Añadir IA cuando el CRM manual funcione. No activar ALLOW_SIGNUP para altas públicas; confirmar el mecanismo de creación del primer administrador y cerrarlo después.
7. Alinear PORT/3000, HOSTNAME=0.0.0.0, dominio HTTPS y healthcheck /api/health. Verificar qué comprueba salud: un 200 no basta para demostrar el recorrido completo.
8. Crear dominio piloto independiente; confirmar DNS y certificados antes de cualquier callback. No asumir que el dominio propuesto ya existe ni modificar los dominios del producto anterior.
9. Observar SUCCESS del despliegue concreto, acceso HTTPS, creación del administrador, configuración de marca, escritura en BD, subida/lectura de archivo y persistencia después de reiniciar. Observar sesiones y conexiones SSE sin buffering excesivo.
10. Configurar backups de BD y medios con retención explícita; hacer una restauración aislada. Registrar versión, ambiente, fecha, resultados y reversión. Con volumen puede haber interrupción durante despliegues; no prometer continuidad sin medirla.

**Salida:** instancia piloto accesible con datos de prueba y evidencia de funcionamiento. Desplegar el CRM no autoriza conectar activos reales, cambiar webhooks existentes o enviar mensajes a clientes.

## 3. WhatsApp y experiencia de ventas

Seleccionar activos de prueba autorizados, permisos y destinatarios permitidos. Usar la app propia y un espacio de revisión, siguiendo las restricciones actuales de Meta. Antes de tocar el callback de una app/WABA compartida, evaluar su alcance y preservar la operación existente. Registrar la configuración y un camino de reversión; no registrar tokens.

Exigir verificación GET con challenge de texto correcto y POST con firma sobre el cuerpo original. El secreto de la URL no reemplaza HMAC. Validar rechazo de firma inválida, eventos duplicados, estado monotónico, tenant correcto y logs sin secretos. Las recetas históricas que permiten firma opcional requieren endurecimiento para esta operación.

Demostrar bandeja con mensaje real autorizado y respuesta recibida, listado/creación/sincronización de plantilla y envío permitido. Verificar opt-in, ventana de 24 horas, baja y handoff humano. El agente inicia apagado y se activa después de probar límites, errores y recuperación; ninguna venta o entrega se da por realizada sin evidencia.

## 4–5. Cumplimiento y onboarding

Inventariar datos, proveedores efectivos, países, finalidad, retención y eliminación. Ajustar las políticas al CRM real; no copiar promesas o canales del Kweekly anterior. Confirmar identidad legal con las fuentes del titular sin publicar documentos fiscales.

Implementar callbacks de desautorización y eliminación con signed_request validado, acuse, estado consultable y ejecución real conforme a retención declarada. Revocar acceso no es lo mismo que eliminar mensajes, archivos y datos. Probar ambos recorridos y accesos de administradores.

Diseñar conexión central e instancia destino explícita. Embedded Signup necesita frontend, intentos con estado/expiración, backend de canje, credenciales cifradas y relación verificable negocio–WABA–número. Verificar la versión vigente antes de implementar; la revisión previa encontró retiro de v2/v3 anunciado para octubre y debe reconfirmarse en la fuente oficial.

No trasladar sin revisar los defectos detectados en Kweekly: espera de interfaz demasiado corta, relación de activos incompleta y selección de tenant ambigua por WABA/número. Suscribir eventos y confirmar lectura posterior, registrar número solo cuando corresponda, distinguir reconexión/coexistencia y evitar asociar activos de clientes al portafolio de Kinetia. Probar al menos dos negocios sin accesos cruzados, duplicados, permisos revocados, token vencido, cancelación y recuperación de errores. No deshabilitar checks para que el video aparente éxito.

## 6–7. Solicitud de Meta

Revalidar Kinetia Agency, negocio y verificación de acceso en Brave. Mantener esta app si sirve al producto final; no crear una nueva por costumbre. Completar plataforma web, dominios y URLs del producto final, Login for Business y configuración de WhatsApp. Alinear la app y la marca mostrada sin presentar el fork como aprobado.

Pedir únicamente los permisos que el recorrido demuestre: whatsapp_business_management y whatsapp_business_messaging como alcance inicial. Los permisos de catálogo, Instagram u otros deben tener una necesidad real y evidencia propia. Revisar en el panel si public_profile se exige en ese momento; una táctica comunitaria no sustituye requisitos actuales.

Preparar usuario de revisor con datos de prueba, acceso estable y pasos en inglés. Grabar dos evidencias: gestión de plantillas para management y envío/recepción real para messaging. Mostrar acciones desde Kweekly CRM y el resultado correspondiente en WhatsApp. Sin secretos ni conversaciones de terceros. Las simulaciones del Laboratorio no sirven como evidencia de entrega.

Resolver publicación y requisitos de prueba en el orden permitido por Meta. Completar gestión de datos de forma veraz y coherente con hosting, IA y soporte efectivos. Guardar un dossier con configuración, videos, textos y checklist. El titular revisa y envía la solicitud. Registrar acuse y resultado; ante rechazo, corregir la causa demostrada y reenviar sin cambiar arbitrariamente todo el diseño. No prometer plazos ni aprobación.

## 8–9. Primer cliente y evolución

Con acceso confirmado, conectar un negocio piloto mediante el recorrido autorizado; sus WABA/número y pago de WhatsApp permanecen en su control según el modelo aplicable. Acordar consentimiento, alcance del agente, intervención humana, responsabilidades, soporte y consumos sin inventar precios. Probar desconexión y eliminación además de venta y mensajería.

Medir entrega, errores, respuesta humana, desconexiones, recuperación y consumo. Elegir después instancias por cliente o SaaS multiempresa, integraciones con el motor Kweekly, cobros y migración. La API de cerebro externo ofrece un punto de integración, pero compatibilidad y resultados se deben demostrar antes de sustituir el producto existente.

## Riesgos y decisiones pendientes

- Railway: ubicación del piloto, permisos, dominio, presupuesto y capacidad aún por confirmar.
- Meta: estado actual, permisos, versión de Embedded Signup y alcance de callbacks compartidos deben revalidarse antes de operar.
- Datos: retención, proveedores, respaldos y responsables legales requieren decisiones documentadas.
- Operación: no abrir altas públicas antes de controles y aislamiento; no usar mensajes del Laboratorio para App Review.
- Upstream: revisar cambios y dependencias periódicamente; conservar atribución y fijar releases propios reproducibles.

## Fuentes y alcance de la evidencia

- Código upstream fijado en [procedencia](procedencia.md) y documentación heredada [README.upstream.md](../../README.upstream.md).
- Vibe Community VIP: /Users/jehusilva/projects/vibe-community-vip/recursos/descomprimidos/03-vocero-starter/vocero-starter/README.md y módulo 09-whatsapp-saas-meta-skills. Se usa su secuencia de infraestructura, revisión y videos; se adapta Coolify a Railway.
- Auditoría anterior: /Users/jehusilva/kinetia/outputs/kweekly-meta-tech-provider-20261003/analisis-y-plan.md. Los estados del panel son observaciones de esa revisión, no garantía del estado futuro.
- [Meta: Tech Providers](https://developers.facebook.com/documentation/business-messaging/whatsapp/solution-providers/get-started-for-tech-providers/), [Embedded Signup](https://developers.facebook.com/documentation/business-messaging/whatsapp/embedded-signup/implementation/), [Access Verification](https://developers.facebook.com/documentation/development/release/access-verification). Consultados previamente mediante Brave; en este turno la consulta web automática fue limitada por Meta. Reconfirmar requisitos en Brave antes de ejecutar etapas Meta.
- [Railway: Dockerfiles](https://docs.railway.com/builds/dockerfiles), [volúmenes](https://docs.railway.com/volumes), [healthchecks](https://docs.railway.com/deployments/healthchecks), [PostgreSQL](https://docs.railway.com/databases/postgresql).
