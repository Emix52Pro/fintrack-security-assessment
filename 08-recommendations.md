# 08 — Recomendaciones Finales

**Decisión que permite tomar este documento:** definir qué debe implementar FinTrack, en qué orden y con los recursos disponibles.

---

## Resumen ejecutivo

La principal exposición de FinTrack se encuentra en la identidad digital. El incidente de phishing demostró que una contraseña robada permitió acceder al correo de Finanzas desde una ubicación y dispositivo anómalos, crear una regla de reenvío y mantener persistencia durante casi seis días. La ausencia de MFA efectivo, acceso condicional y alertas convirtió una credencial comprometida en un incidente prolongado.

La prioridad inmediata es reducir los riesgos R1 y R6 mediante MFA, revocación de sesiones, bloqueo de reenvíos externos, alertas de acceso anómalo y un procedimiento de respuesta definido. Después deben reforzarse la autenticación de clientes, la seguridad de la API, la gestión de secretos y la capacidad de recuperación ante malware o ransomware.

No se recomienda iniciar con soluciones empresariales costosas ni con una certificación formal. FinTrack tiene 45 empleados, cuatro personas en TI y ningún equipo dedicado de seguridad; por tanto, debe implementar primero controles sostenibles, medibles y de alto impacto.

---

## Prioridades

| Prioridad | Objetivo | Riesgos |
|-----------|----------|---------|
| **1** | Proteger identidades y detectar compromisos en minutos. | R1, R6 |
| **2** | Reducir accesos automatizados y abuso de la API pública. | R2, R4 |
| **3** | Limitar dependencias externas y mejorar recuperación. | R3, R5 |

---

## Hoja de ruta

| Cuándo | Acción | Riesgo que reduce | Esfuerzo |
|--------|--------|-------------------|----------|
| **Esta semana** | Activar MFA en todas las cuentas internas. | R1 | Bajo |
| **Esta semana** | Revocar sesiones activas y revisar reglas de reenvío externo. | R1, R6 | Bajo |
| **Esta semana** | Crear alertas por ubicación imposible, dispositivo desconocido, actividad nocturna y reenvíos externos. | R1, R6 | Bajo |
| **Esta semana** | Formalizar responsables y aplicar el playbook de phishing. | R6 | Bajo |
| **Este mes** | Configurar acceso condicional por ubicación, riesgo y dispositivo. | R1 | Medio |
| **Este mes** | Revisar privilegios y separar cuentas administrativas. | R1 | Bajo |
| **Este mes** | Aplicar límites de intentos, alertas de nuevo dispositivo y bloqueo de contraseñas filtradas. | R2 | Medio |
| **Este mes** | Inventariar proveedores, integraciones, claves y responsables. | R3 | Bajo |
| **Este mes** | Centralizar logs de identidad, correo, API, nube y administración. | R6 | Medio |
| **Este mes** | Validar copias de seguridad y documentar tiempos de recuperación. | R5 | Bajo |
| **Este trimestre** | Implementar MFA adaptativo para transferencias y cambios sensibles. | R2 | Medio |
| **Este trimestre** | Migrar claves y tokens a un gestor centralizado de secretos. | R3 | Medio |
| **Este trimestre** | Revisar autorización por objeto y función en los endpoints críticos. | R4 | Medio |
| **Este trimestre** | Implementar protección de endpoints y ejecutar una prueba de restauración. | R5 | Medio |
| **Este trimestre** | Realizar un simulacro de phishing y medir detección y contención. | R1, R6 | Bajo |
| **12 meses** | Evaluar un servicio MDR o SOC externo según el volumen de alertas y capacidad del equipo. | R5, R6 | Alto |
| **12 meses** | Revisar madurez de controles y decidir si FinTrack está preparada para una iniciativa formal de cumplimiento. | R1–R6 | Medio |

---

## Indicadores de éxito

| Indicador | Meta |
|-----------|------|
| Cuentas internas protegidas con MFA | 100 % |
| Cuentas administrativas separadas | 100 % |
| Tiempo de reconocimiento de un incidente alto | Menos de 15 minutos |
| Tiempo de contención inicial | Menos de 30 minutos |
| Reglas de reenvío externo no autorizadas | 0 |
| Integraciones con propietario y credencial inventariada | 100 % |
| Endpoints críticos con pruebas de autorización | 100 % |
| Restauraciones de respaldo verificadas | Una por trimestre |
| Simulacros de phishing | Uno por trimestre |
| Acciones correctivas cerradas en plazo | Al menos 90 % |

---

## Riesgo residual

La implementación de estas recomendaciones no elimina todos los ataques. El phishing, el abuso de credenciales y los errores de lógica seguirán siendo posibles. El objetivo es que una contraseña robada no sea suficiente, que un acceso anómalo genere una alerta inmediata, que el alcance del atacante sea limitado y que FinTrack pueda recuperarse con evidencia y procedimientos definidos.

---

## Lo que deliberadamente no recomendamos

| Descartado | Por qué |
|-----------|---------|
| **SIEM empresarial y SOC 24/7 en la primera fase** | El costo y la complejidad son desproporcionados. Primero deben funcionar las alertas nativas y la centralización básica de logs. |
| **Migración completa de infraestructura** | No es necesaria para cerrar los caminos de ataque prioritarios y consumiría recursos críticos. |
| **Plataforma especializada de seguridad de API** | Los controles nativos, la autorización en backend y las pruebas automáticas ofrecen mayor valor inicial. |
| **Llaves físicas para todos desde el primer día** | Se priorizan en Finanzas, TI y administradores; el resto puede iniciar con MFA mediante aplicación autenticadora. |
| **Certificación ISO 27001 inmediata** | FinTrack debe demostrar primero que sus controles, políticas y procesos funcionan de forma sostenida. |
| **Capacitación como único control contra phishing** | La formación reduce errores, pero no sustituye MFA, acceso condicional, mínimo privilegio ni monitoreo. |
| **Controles especializados contra actores estatales** | No corresponden al perfil de amenaza prioritario ni al presupuesto actual. |

---

## Conclusión

FinTrack no necesita comenzar por la herramienta más avanzada, sino por cerrar el camino que ya fue explotado. La combinación de MFA, acceso condicional, mínimo privilegio, alertas específicas, centralización de logs y un playbook operativo ofrece la mayor reducción de riesgo con el menor esfuerzo sostenible.

La mejora central puede resumirse así:

> **Una identidad comprometida no debe convertirse en acceso persistente, y un acceso anómalo no debe permanecer invisible durante días.**
