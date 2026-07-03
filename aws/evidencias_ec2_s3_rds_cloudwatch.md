# 📂 Evidencias de Configuración de Servicios AWS

Este documento contiene la descripción técnica y la referencia de auditoría para cada uno de los servicios principales desplegados en la infraestructura elástica de **Comercial Nova**. Todas las pruebas e inspecciones visuales fueron convalidadas directamente en el entorno de desarrollo bajo Pop!_OS.

---

## 💻 1. Capa de Cómputo: Amazon EC2
* **Recurso Identificado:** `EC2-WordPress-Primary-David`
* **ID de la Instancia:** `i-0447f138b61ff1897`
* **Tipo de Instancia:** `t3.micro` (Arquitectura x86_64)
* **Zona de Disponibilidad:** `us-east-1a`
* **Descripción de la Configuración:** Servidor basal aprovisionado con Amazon Linux 2023. Aloja de manera monolítica el stack LAMP (Apache, PHP 8.x, motor MariaDB de contingencia) y el core de WordPress. Las reglas de firewall restringen el acceso perimetral directo, permitiendo tráfico únicamente desde el balanceador de carga (`ALB-ComercialNova-David`).
* **Evidencia Visual Requerida:** *(Mapear aquí la captura de tu lista de instancias en ejecución: `capturas_servicios/evidencia_instancias_ec2.png`)*

---

## 🪣 2. Capa de Almacenamiento: Amazon S3
* **Nombre del Bucket:** `comercialnova-media-wd-01`
* **Región Global:** `us-east-1` (Norte de Virginia)
* **Estado de Acceso Público:** Bloqueo de acceso público masivo activado (*Block all public access*).
* **Descripción de la Configuración:** Almacenamiento elástico configurado con políticas de cifrado basal en reposo administrado por Amazon S3 (SSE-S3). Sirve como el repositorio persistente centralizado para los archivos estáticos y la carpeta de medios (`wp-content/uploads`) de la corporación.
* **Evidencia Visual Requerida:** *(Mapear aquí la captura de tu bucket creado en la consola de S3: `capturas_servicios/evidencia_bucket_s3.png`)*

---

## 📊 3. Capa de Observabilidad: Amazon CloudWatch
* **Componente 1:** Dashboard de Métricas Personalizado (`Dashboard-ComercialNova`)
* **Componente 2:** Alarma Estática de Estrés (`Alarma-CPU-70-David`)
* **Métrica Auditada:** `CPUUtilization` (Espacio de nombres: `AWS/EC2`)
* **Condición de Alerta:** Utilización media de CPU superior al 70% durante un periodo continuo de evaluación de 5 minutos.
* **Descripción de la Configuración:** Panel de observabilidad en tiempo real acoplado a la infraestructura para monitorear el rendimiento basal del servidor web. La alarma está diseñada formalmente para interactuar con las políticas de escalado horizontal del Auto Scaling Group.
* **Evidencia Visual Requerida:** *(Mapear aquí tu captura del gráfico o alarma de CloudWatch: `capturas_servicios/evidencia_cloudwatch.png`)*

---

## 🛑 4. Nota sobre Capa de Datos: Amazon RDS
* **Estado del Recurso:** No Desplegado (Bloqueo de Gobernanza IAM).
* **Evidencia del Incidente:** Durante la fase de aprovisionamiento del clúster de base de datos relacional MySQL/Aurora, la infraestructura arrojó una denegación explícita de permisos (`rds:CreateDBInstance`) vinculada al rol `policy/Pvoclabs2` restringido por el entorno académico de **AWS Academy Learner Lab**.
* **Estrategia de Contingencia Aplicada:** Conforme a los lineamientos de la rúbrica del examen final, la restricción técnica se justificó con evidencia de auditoría. Se procedió a mitigar el bloqueo instalando y securizando MariaDB de manera interna en el almacenamiento de bloques EBS de la instancia EC2 principal, garantizando la total disponibilidad y comunicación local del CMS WordPress.