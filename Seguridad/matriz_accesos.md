```markdown
# Matriz de Seguridad y Reglas de Firewalls (Security Groups)

| Origen | Puerto | Protocolo | Propósito | Impacto Perimetral |
| :--- | :--- | :--- | :--- | :--- |
| `0.0.0.0/0` | 80 | HTTP | Tráfico Web Público | Acceso elástico global al portal |
| `0.0.0.0/0` | 443 | HTTPS | Navegación Cifrada | Seguridad de datos en tránsito |
| Bloqueado | 22 | SSH | Administración Remota | Reducción de la superficie de ataque |