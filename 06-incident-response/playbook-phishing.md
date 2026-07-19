# Playbook — Incidente de phishing

Procedimiento paso a paso para el incidente más probable de FinTrack.

**Mitiga:** R1 — Compromiso de identidad interna mediante phishing; R6 — Detección tardía y respuesta insuficiente  
**Responsable principal:** Responsable de Infraestructura  
**Cuándo se activa:** cuando un empleado reporta haber abierto un enlace, descargado un archivo, entregado credenciales o aprobado un acceso sospechoso; o cuando una alerta detecta inicio de sesión anómalo, regla de reenvío externo o dispositivo desconocido.

---

## Objetivo

Detener el uso de credenciales robadas, preservar evidencia y determinar si el atacante accedió a correo, datos, transferencias o servicios internos.

---

## Pasos

1. **Recibir el reporte sin culpar al usuario.** Registrar quién reporta, qué mensaje recibió, qué acción realizó y a qué hora.
2. **Preservar el correo.** Guardar mensaje original, remitente, asunto, enlace, adjuntos y encabezados. No reenviar el correo sospechoso de forma normal.
3. **Abrir el incidente.** Asignar identificador, severidad y responsables.
4. **Revocar todas las sesiones activas.** Invalidar sesiones web, móviles, tokens y aplicaciones autorizadas.
5. **Cambiar la contraseña por un canal seguro.** No reutilizar una clave anterior y activar o restablecer MFA.
6. **Revisar reglas y persistencia.** Eliminar reenvíos externos, delegaciones, filtros, aplicaciones OAuth, tokens o métodos MFA desconocidos.
7. **Examinar los últimos siete días de actividad.** Revisar IP, ubicación, dispositivo, horario, accesos al correo, descargas, privilegios y acciones administrativas.
8. **Buscar señales del caso FinTrack.** Priorizar ubicación imposible, dispositivo headless/script, actividad nocturna, regla de reenvío y accesos repetidos desde la misma IP.
9. **Determinar el alcance.** Verificar si el atacante accedió a datos de clientes, transferencias, API, panel administrativo o integraciones.
10. **Buscar el mismo correo en otras cuentas.** Retirar el mensaje, bloquear remitente, dominio, URL y archivo cuando sea seguro hacerlo.
11. **Aislar el equipo si hubo descarga o ejecución.** Mantenerlo encendido pero desconectado de la red hasta la revisión.
12. **Escalar de inmediato si existe fraude o exposición de datos.** Informar a Dirección, Finanzas, Legal y proveedor correspondiente.
13. **Restaurar el acceso de forma controlada.** Confirmar MFA, permisos correctos y ausencia de sesiones o reglas maliciosas.
14. **Monitorear durante 72 horas.** Revisar nuevos intentos, reglas, cambios de contraseña, accesos anómalos y actividad relacionada.
15. **Cerrar solo con evidencia suficiente.** Documentar alcance, impacto, acciones, responsables y pendientes.

---

## Lista rápida de los primeros 10 minutos

| Minuto | Acción |
|--------|--------|
| 0–2 | Escuchar el reporte y registrar la hora |
| 2–4 | Preservar el correo o la alerta |
| 4–6 | Revocar sesiones y bloquear acceso |
| 6–8 | Cambiar contraseña y asegurar MFA |
| 8–10 | Revisar reglas de reenvío y accesos recientes |

---

## Criterios de escalamiento

Escalar como incidente **alto o crítico** cuando se confirme cualquiera de los siguientes:

- Inicio de sesión exitoso desde ubicación o dispositivo anómalo.
- Regla de reenvío hacia una dirección externa.
- Acceso a correo financiero o datos de clientes.
- Intento de acceso administrativo.
- Transferencia o cambio de datos no autorizado.
- Más de una cuenta afectada.
- Malware ejecutado.
- Falta de logs suficientes para determinar el alcance.

---

## Evidencia que debe recopilarse

- Correo original y encabezados.
- URL, dominio y dirección del remitente.
- Usuario afectado.
- Fecha y hora de interacción.
- IP, ubicación y dispositivo.
- Inicios de sesión exitosos y fallidos.
- Reglas de correo y aplicaciones autorizadas.
- Cambios de contraseña, MFA y privilegios.
- Archivos descargados o ejecutados.
- Acciones realizadas por el atacante.
- Medidas de contención y hora exacta.

---

## Qué NO hacer

- No culpar ni amenazar al empleado que reporta.
- No pedir que elimine el correo antes de conservar evidencia.
- No reenviar enlaces o adjuntos sospechosos a otros empleados.
- No limitarse a cambiar la contraseña; también deben revocarse sesiones y tokens.
- No apagar un equipo con posible malware antes de decidir cómo preservar evidencia.
- No comunicar públicamente el incidente sin autorización.
- No cerrar el caso solo porque el siguiente inicio de sesión falló.
- No asumir que no hubo impacto por ausencia de pérdida económica visible.

---

## Criterios de cierre

El incidente puede cerrarse cuando:

1. Las sesiones y credenciales comprometidas fueron invalidadas.
2. No quedan reglas, tokens, aplicaciones o métodos MFA desconocidos.
3. El alcance fue revisado en correo, identidad, API, administración y transferencias.
4. Se determinó el impacto confirmado y potencial.
5. Las cuentas relacionadas fueron monitoreadas durante 72 horas.
6. Las acciones correctivas tienen responsable y fecha.

---

## Después

Para el postmortem se documenta:

- Línea de tiempo completa.
- Vector de entrada.
- Tiempo de detección y contención.
- Cuentas, datos y sistemas afectados.
- Controles que fallaron.
- Controles que funcionaron.
- Evidencia que faltó.
- Acciones correctivas y responsables.
- Cambios al playbook, alertas y políticas.

---

## Aplicación al incidente simulado

En el caso de `a.torres`, este playbook habría activado la contención al detectar el primer inicio de sesión desde Moscú o la creación de la regla de reenvío externo. La revocación de sesiones y el cambio de credenciales debieron realizarse el mismo día, no seis días después.

---
