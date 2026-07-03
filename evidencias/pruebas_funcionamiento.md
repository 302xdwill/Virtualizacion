# 🧪 Plan de Pruebas y Evidencias de Funcionamiento

Este documento recopila las pruebas de conectividad, carga y validación perimetral realizadas sobre la infraestructura cloud de **Comercial Nova**. Todas las capturas de auditoría reflejan el entorno del estudiante sobre Pop!_OS con la hora del sistema visible para garantizar la autoría.

## 🏁 Prueba 1: Acceso Público vía DNS del Balanceador (ELB)
* **Objetivo:** Verificar que el Application Load Balancer (`ALB-ComercialNova-David`) reciba el tráfico en el puerto 80 y lo enrute correctamente al stack web.
* **Resultado:** **EXITOSO**. Al ingresar al DNS elástico provisto por AWS, el balanceador cargó limpiamente la página de inicio del portal corporativo sin latencia ni pérdida de paquetes.
* **Archivo de Evidencia:** `capturas_servicios/evidencia_alb_wordpress.png` (Corresponde a la captura del portal en vivo).

## 📊 Prueba 2: Validación del Panel de Administración (WordPress Dashboard)
* **Objetivo:** Comprobar la correcta conexión interna entre el servidor web Apache, el intérprete PHP y el motor de base de datos local MariaDB (contingencia implementada por bloqueo de RDS).
* **Resultado:** **EXITOSO**. Se completó el asistente de instalación nativo, se accedió al panel de control `/wp-admin/` y se procedió con la publicación del post oficial de lanzamiento.
* **Archivo de Evidencia:** `capturas_servicios/evidencia_dashboard_post.png` (Corresponde a la captura del editor de WordPress).

## 🛠️ Prueba 3: Estado Saludable en los Target Groups
* **Objetivo:** Auditar que las comprobaciones de estado (*Health Checks*) estén en verde tras aplicar el ajuste de códigos de éxito (`200,301,302`).
* **Resultado:** **EXITOSO**. El balanceador dejó de emitir el error de pasarela *502 Bad Gateway* y marcó la instancia principal en estado **Healthy**, asimilando las redirecciones internas del CMS.
* **Archivo de Evidencia:** `capturas_servicios/evidencia_target_groups.png`

## 📉 Prueba 4: Auditoría de Costos (AWS Billing)
* **Objetivo:** Validar el consumo acumulado de los recursos desplegados durante la sesión del laboratorio para asegurar el cumplimiento del presupuesto estimado.
* **Resultado:** **EXITOSO**. Acceso verificado al módulo de facturación real de AWS, registrando las métricas financieras base del aprovisionamiento.
* **Archivo de Evidencia:** `capturas_servicios/evidencia_billing_real.png`

---

### 📂 Organización de Archivos en esta Carpeta:
Asegúrate de que tus imágenes estén renombradas y guardadas dentro de la subcarpeta de la siguiente manera para mantener la consistencia del Markdown:
* `/evidencias/capturas_servicios/evidencia_alb_wordpress.png`
* `/evidencias/capturas_servicios/evidencia_dashboard_post.png`
* `/evidencias/capturas_servicios/evidencia_target_groups.png`
* `/evidencias/capturas_servicios/evidencia_billing_real.png`