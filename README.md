# Portal Corporativo WordPress en Alta Disponibilidad - Comercial Nova

## 👤 Datos del Estudiante
* **Estudiante:** Ortiz Mamani William David
* **Curso:** Virtualización de Servicios Tecnológicos
* **Institución:** Universidad Peruana Unión (UPeU)
* **Docente:** Ing. Fredy Huanca Torres
* **Fecha:** 2 de julio de 2026

## 🎯 1. Problema Planteado y Alcance
La empresa "Comercial Nova" requería el despliegue urgente de su nuevo portal web corporativo utilizando WordPress. Los requerimientos obligatorios exigían una infraestructura en la nube capaz de mitigar puntos únicos de fallo (SPOF), aislar las bases de datos del perímetro público, garantizar el almacenamiento elástico de medios y proveer métricas en tiempo real bajo un riguroso análisis de costos mensuales.

## 🏗️ 2. Arquitectura Propuesta y Servicios Utilizados
Se implementó una arquitectura desacoplada y redundante basada en zonas de disponibilidad distribuidas (Multi-AZ) dentro de la región `us-east-1` (Norte de Virginia):
* **Amazon VPC:** Red propia con segmentación de subredes públicas y privadas, tablas de ruteo dedicadas e Internet Gateway (`igw`).
* **Amazon ELB (Application Load Balancer):** Punto único de entrada elástica (`ALB-ComercialNova-David`) encargado de interceptar las peticiones HTTP del puerto 80 y balancear la carga hacia los destinos saludables.
* **Amazon EC2:** Instancias de cómputo `t3.micro` ejecutando Amazon Linux 2023 y el stack LAMP (Apache, PHP 8.x, MySQL/MariaDB nativo).
* **Amazon S3:** Bucket elástico global (`comercialnova-media-wd-01`) para almacenamiento seguro de recursos multimedia de la organización.
* **Amazon CloudWatch:** Panel de control métrico y alarmas estáticas para la observabilidad perimetral.

## 🚀 3. Pasos para Reproducir el Despliegue
1. Crear la VPC personalizada utilizando el asistente de topología elástica en AWS.
2. Desplegar la instancia EC2 principal inyectando el script de automatización LAMP en la sección de *User Data*.
3. Provisionar el bucket S3 con políticas de bloqueo de acceso público masivo.
4. Crear un Target Group HTTP en el puerto 80 agregando la instancia principal y configurando los códigos de éxito del Health Check en `200,301,302` para asimilar las redirecciones internas de WordPress.
5. Lanzar el Application Load Balancer en las subredes públicas y vincularlo al Target Group.

## 🔗 4. URL de Acceso Corporativo
* **DNS elástico del ALB:** `http://alb-comercialnova-david-1728357022.us-east-1.elb.amazonaws.com`

## 🚨 5. Limitaciones Conocidas y Ruta de Contingencia
* **Restricción de Amazon RDS:** Durante el despliegue del servicio administrado relacional, las políticas IAM de AWS Academy (`policy/Pvoclabs2`) arrojaron una denegación explícita (`rds:CreateDBInstance`). Siguiendo los lineamientos de la guía, se aplicó la contingencia de despliegue sobre cómputo, instalando y securizando MariaDB de manera interna en la instancia EC2, garantizando el funcionamiento transparente del CMS.
* **Restricción de Auto Scaling:** El Auto Scaling Group fue configurado basándose en la métrica de CPU al 70%. Al utilizar una AMI limpia sin la persistencia sincronizada de la base de datos monolítica local, se desvinculó temporalmente el plano de datos del Target Group del ALB para salvaguardar la sesión activa de WordPress y evitar errores de pasarela 502/503.

## 💡 6. Estrategias y Lecciones Aprendidas
* **Seguridad:** Uso del principio de mínimo privilegio eliminando accesos SSH y aislando los grupos de seguridad del backend.
* **Costos:** Dimensionamiento exacto en capa gratuita para asegurar compatibilidad presupuestaria.
* **Lección Técnica:** Un Ingeniero de Sistemas debe estar preparado para adaptar la arquitectura lógica ante bloqueos de gobernanza o permisos de infraestructura sin detener la entrega continua del servicio.