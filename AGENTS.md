# Kweekly CRM — instrucciones de trabajo

Lee README.md, docs/kweekly/plan-general.md y CLAUDE.md. Conserva la constitución heredada salvo una decisión explícita documentada. Este fork usa Railway como destino piloto; las referencias heredadas a Coolify describen el upstream.

Producto: Kweekly CRM, Un producto de Kinetia. Perfil: /Users/jehusilva/kinetia/Design System/profiles/kweekly.md. Conserva personalización por negocio; no cambies agentes de clientes por un cambio de marca. LICENSE y atribución upstream permanecen.

Una instancia piloto = un negocio. No presentes organization_id o ALLOW_SIGNUP como prueba de onboarding multiempresa. La aprobación de Meta exige verificación, permisos, funcionamiento y evidencia propios.

El Kweekly anterior está en ../kweekly: úsalo como referencia de lectura; no lo migres, despliegues ni modifiques por trabajar aquí. No copies sus secretos.

Antes de operar Railway identifica proyecto, ambiente y servicio exactos. Usa use-railway. No reportes despliegue exitoso sin SUCCESS y comprobaciones reales. Evita modificar los callbacks actuales de Meta hasta revisar impacto. Sincronización GitHub no significa publicación de una instancia.

Para WhatsApp/Meta usa whatsapp-saas-meta-infra, whatsapp-meta-app-review y whatsapp-app-review-video según la etapa. Verifica documentos públicos vigentes; distingue comprobaciones locales de evidencia en vivo. No publiques App Review ni envíes mensajes a terceros sin alcance autorizado.
