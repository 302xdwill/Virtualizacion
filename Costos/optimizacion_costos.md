# Plan de Optimización Financiera y Estimación Mensual

## Desglose Base de Producción Continua
* **Amazon EC2 (Cómputo Multi-AZ):** $14.98 USD/mes
* **Amazon EBS (Discos GP3):** $1.28 USD/mes
* **Application Load Balancer (ALB):** $16.20 USD/mes
* **Amazon S3 (Almacenamiento Standard):** $1.15 USD/mes
* **Costo Total Proyectado:** **$33.61 USD / mes**

## Estrategias Concretas de Ahorro de Presupuesto Corporativo
1. **Programación Horaria (AWS Instance Scheduler):** Apagar instancias fuera del horario laboral, reduciendo el gasto de cómputo en un 72.2%.
2. **Ciclo de Vida S3 (Lifecycle Policies):** Mover medios fríos a S3 Glacier Flexible Retrieval tras 30 días, bajando el coste de almacenamiento un 80%.
3. **Rightsizing de EBS:** Migrar volúmenes de almacenamiento en bloques a configuraciones GP3 nativas, ahorrando un 20% estructural en discos.