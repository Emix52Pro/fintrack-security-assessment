# 07 — Postmortem: Incidente de phishing

**Cultura:** este postmortem es sin culpables (*blameless*). El objetivo es identificar las fallas de proceso y control que permitieron el incidente, no responsabilizar al empleado afectado.

**Incidente relacionado:** R1 — Compromiso de identidad interna mediante phishing; R6 — Detección tardía y respuesta insuficiente  
**Severidad:** Alta  
**Periodo analizado:** 14 al 20 de abril de 2026

---

## Resumen

La cuenta corporativa `a.torres`, perteneciente al área de Finanzas, fue comprometida después de un ataque de phishing. El atacante inició sesión desde Moscú mediante la IP `203.0.113.77`, creó una regla de reenvío externo y mantuvo acceso durante casi seis días. El incidente fue detectado por un compañero al observar una respuesta extraña en un hilo de correo, no por una alerta técnica. IT cambió la contraseña, eliminó la regla y bloqueó el siguiente intento de acceso.

---

## Indicadores principales

| Indicador | Resultado |
|-----------|-----------|
| Cuenta afectada | `a.torres` — Andrea Torres, Finanzas |
| IP sospechosa | `203.0.113.77` |
| Ubicación sospechosa | Moscú, Rusia |
| Dispositivo | Desconocido — headless/script |
| Eventos desde la IP sospechosa | 13 |
| Inicios de sesión sospechosos exitosos | 6 |
| Accesos al correo | 4 |
| Intentos de acceso administrativo | 1, denegado |
| Tiempo hasta el reporte | 5 días, 18 horas y 11 minutos |
| Tiempo hasta el cambio de contraseña | 5 días, 18 horas y 49 minutos |
| Permanencia de la regla de reenvío | 5 días, 18 horas y 46 minutos |
| Pérdida económica confirmada | No confirmada |

---

## Línea de tiempo

| Fecha y hora | Evento |
|--------------|--------|
| **14/04/2026 14:52** | La cuenta se reautentica legítimamente desde Quito. |
| **14/04/2026 15:03** | Primer inicio de sesión sospechoso desde Moscú con un dispositivo headless/script. |
| **14/04/2026 15:07** | El atacante crea una regla de reenvío automático hacia una dirección externa. |
| **15/04/2026 02:20** | Primer acceso nocturno confirmado al correo. |
| **16/04/2026 03:09** | El atacante intenta acceder al panel administrativo; el sistema lo deniega por falta de rol. |
| **17/04/2026 01:55** | Nuevo acceso al correo desde la IP sospechosa. |
| **18/04/2026 04:30** | Tercer acceso nocturno al correo. |
| **19/04/2026 04:05** | Cuarto acceso al correo desde Moscú. |
| **20/04/2026 09:14** | Un compañero reporta una respuesta extraña en un hilo de correo de `a.torres`. |
| **20/04/2026 09:41** | Infraestructura confirma el acceso no autorizado. |
| **20/04/2026 09:52** | IT fuerza el cambio de contraseña. |
| **20/04/2026 09:53** | IT elimina la regla de reenvío externo. |
| **20/04/2026 10:10** | El siguiente intento desde Moscú falla porque la credencial fue invalidada. |

---

## Impacto

- **Confidencialidad:** se confirmó acceso no autorizado al correo corporativo de Finanzas, con posible exposición de información interna y datos relacionados con clientes.
- **Integridad:** el atacante modificó la configuración del correo al crear una regla de reenvío externo y pudo intervenir en conversaciones.
- **Disponibilidad:** no se registró una interrupción general de la plataforma; el impacto se limitó al restablecimiento y aseguramiento de la cuenta.
- **Negocio:** no se confirmó pérdida económica, pero el acceso prolongado y la evidencia limitada impidieron descartar completamente exposición o uso indebido de información.
- **Reputación:** una filtración o fraude asociado a una cuenta financiera habría afectado directamente la confianza de los clientes.

---

## Causa raíz

La causa raíz no fue que un empleado interactuara con un correo de phishing. La causa fue que **una contraseña robada era suficiente para iniciar sesión desde un país y dispositivo anómalos sin una segunda verificación ni bloqueo automático**.

Factores contribuyentes:

1. MFA y acceso condicional no estaban aplicados de forma efectiva.
2. No existían alertas por viaje imposible, dispositivo desconocido o actividad nocturna.
3. Se permitía crear reglas de reenvío externo sin aprobación ni alerta.
4. Los registros no estaban centralizados ni eran revisados de forma operativa.
5. No existía un plan escrito ni un playbook para responder a cuentas comprometidas.
6. La detección dependía de que una persona notara un comportamiento extraño.

---

## Qué funcionó / qué no

| Funcionó | No funcionó |
|----------|-------------|
| El principio de mínimo privilegio impidió el acceso al panel administrativo. | Las credenciales robadas permitieron varios inicios de sesión exitosos. |
| Un compañero identificó el comportamiento extraño y lo escaló a IT. | No hubo alerta por acceso simultáneo desde Quito y Moscú. |
| IT confirmó el compromiso y ejecutó la contención. | No hubo alerta por dispositivo headless/script ni actividad nocturna. |
| El cambio de contraseña bloqueó el siguiente intento del atacante. | La regla de reenvío externo permaneció activa casi seis días. |
| La regla maliciosa fue localizada y eliminada. | No existía un proceso formal de respuesta ni responsables previamente definidos. |
| Los logs permitieron reconstruir los hitos principales. | La evidencia disponible no permitió confirmar todo el contenido consultado o reenviado. |

---

## Acciones correctivas

| Acción | Dueño | Plazo | Riesgo que reduce |
|--------|-------|-------|-------------------|
| Activar MFA en todas las cuentas internas y priorizar factores resistentes al phishing en Finanzas y TI. | Infraestructura | Esta semana | R1 |
| Configurar acceso condicional por ubicación, dispositivo, riesgo y viaje imposible. | Infraestructura | Este mes | R1 |
| Bloquear o alertar inmediatamente la creación de reglas de reenvío externo. | Infraestructura | Esta semana | R1, R6 |
| Centralizar logs de identidad, correo, API y administración, con alertas y responsables definidos. | Infraestructura + Desarrollo | Este mes | R6 |
| Aplicar el plan de respuesta y el playbook de phishing desarrollados en este repositorio. | Infraestructura + Soporte | Esta semana | R1, R6 |
| Revisar trimestralmente privilegios y mantener separadas las cuentas administrativas. | Infraestructura | Trimestral | R1 |
| Ejecutar simulaciones de phishing y reforzar el canal de reporte sin culpabilización. | Soporte TI | Trimestral | R1 |
| Preservar registros suficientes para determinar accesos, cambios y alcance de futuros incidentes. | Infraestructura | Este mes | R6 |

---

## Riesgo residual

Después de implementar las acciones, el phishing seguirá siendo posible y un empleado todavía puede entregar información. Sin embargo, las credenciales robadas no deberían permitir acceso prolongado, la creación de persistencia debería generar una alerta y el equipo tendría un procedimiento definido para contener el incidente en minutos.

---

## Lección principal

> El incidente no permaneció activo seis días porque el phishing fuera sofisticado, sino porque FinTrack no validaba suficientemente la identidad ni detectaba comportamientos incompatibles con el uso normal de la cuenta.

---

## Estado de cierre

El incidente se considera **contenido** porque la contraseña fue cambiada, la regla de reenvío fue eliminada y el siguiente acceso del atacante falló. Las acciones correctivas permanecen abiertas hasta que existan pruebas de MFA, alertas, centralización de logs y simulación del playbook.

---

