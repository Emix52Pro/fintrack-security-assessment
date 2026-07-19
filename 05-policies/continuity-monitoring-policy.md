# Política de continuidad, monitoreo y respuesta

**Mitiga:** R5 — Interrupción por malware o ransomware; R6 — Detección tardía y respuesta insuficiente  
**Responsable:** Responsable de Infraestructura de TI  
**Aplica a:** equipos, correo, identidad, nube, API, bases de datos, copias de seguridad y personal de respuesta  
**Última revisión:** 2026-07-18

## Propósito

Detectar incidentes con rapidez, limitar su propagación y recuperar los servicios críticos sin improvisación.

## Regla

1. Mantener protección de endpoints, actualizaciones críticas y restricción de privilegios locales en equipos corporativos.
2. Realizar copias de seguridad de datos y configuraciones críticas, conservando al menos una copia aislada del entorno principal.
3. Probar trimestralmente la restauración de un servicio o conjunto de datos crítico.
4. Centralizar registros de identidad, correo, API, administración y nube con una retención mínima definida.
5. Crear alertas para acceso desde ubicación imposible, dispositivo desconocido, actividad nocturna, reenvío externo, múltiples fallos y cambios de privilegios.
6. Asignar a cada alerta una severidad, responsable, tiempo objetivo y acción inicial.
7. Ante phishing confirmado, revocar sesiones, cambiar credenciales, eliminar reglas maliciosas, revisar actividad reciente y preservar evidencia.
8. Registrar cada incidente con cronología, alcance, decisiones, evidencias y acciones correctivas.
9. Actualizar el plan y los playbooks después de cada incidente o simulacro relevante.

## Excepciones

Si un sistema no puede enviar registros o recibir protección de endpoints, su propietario debe notificar a Infraestructura, documentar el riesgo, aplicar segmentación o monitoreo compensatorio y fijar una fecha de corrección. Si una copia no puede completarse, se escala el mismo día y se ejecuta una copia alternativa.

## Verificación

Infraestructura revisa diariamente las alertas críticas y semanalmente el estado de registros, protección de endpoints y copias. Cada trimestre ejecuta una restauración y un ejercicio de phishing. Se conservan resultados, tiempos de respuesta, fallas detectadas y acciones pendientes.
