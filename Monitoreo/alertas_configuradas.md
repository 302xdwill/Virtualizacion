# Configuración de Observabilidad con CloudWatch

* **Métrica Monitoreada:** `CPUUtilization` de la capa de cómputo EC2.
* **Umbral Estático:** Mayor al 70% durante un período de evaluación continuo de 5 minutos.
* **Acción de Escalabilidad vinculada en ASG:** Disparar política de escalado horizontal para aprovisionar hasta un máximo de 3 instancias en paralelo si se vulnera el límite de rendimiento basal.