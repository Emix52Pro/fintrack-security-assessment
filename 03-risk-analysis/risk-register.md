# 03 — Registro de Riesgos

**Decisión que permite tomar este documento:** en qué orden gastar el esfuerzo limitado del equipo.

> Regla: un control sin riesgo asociado no entra al informe. Una política
> sin un riesgo que la exija, tampoco. Seis riesgos bien argumentados valen
> más que veinte listados.

---

## Resumen

| ID | Riesgo | Prob. | Impacto | Nivel | Control principal |
|----|--------|-------|---------|-------|-------------------|
| R1 | Compromiso de identidad interna mediante phishing | Alta | Alto | **Crítico** | C1 — Protección de identidad y acceso |
| R2 | Acceso a cuentas de clientes mediante credential stuffing | Media | Alto | **Alto** | C2 — Protección de autenticación de clientes |
| R3 | Compromiso de proveedores o integraciones externas | Media | Alto | **Alto** | C3 — Gestión de terceros y secretos |
| R4 | Abuso o autorización incorrecta en la API pública | Media | Alto | **Alto** | C4 — Seguridad de API |
| R5 | Interrupción por malware o ransomware | Media | Alto | **Alto** | C5 — Protección, respaldo y recuperación |
| R6 | Detección tardía y respuesta insuficiente | Alta | Alto | **Crítico** | C6 — Monitoreo y respuesta a incidentes |

---

## R1 · Compromiso de identidad interna mediante phishing

| Campo | Valor |
|-------|-------|
| **Descripción** | Un atacante roba credenciales o una sesión de un empleado y utiliza su identidad para acceder al correo y a servicios internos. |
| **Activos** | A4 directamente; A1 y A2 como impacto posterior. |
| **Propiedad violada (CID)** | Confidencialidad e integridad. |
| **Probabilidad** | **Alta** — el escenario ya ocurrió y no existían alertas ni controles suficientes para impedir el acceso con credenciales robadas. |
| **Impacto** | **Alto** — puede exponer información financiera, permitir fraude y facilitar acceso a funciones administrativas. |
| **Nivel** | **Crítico** |
| **Escenario concreto** | Un empleado de Finanzas entrega sus credenciales en una página falsa. El atacante inicia sesión desde Moscú, crea una regla de reenvío y mantiene acceso durante seis días. |
| **Control** | **C1 — Protección de identidad y acceso:** MFA, acceso condicional, revocación de sesiones, mínimo privilegio y bloqueo de dispositivos de alto riesgo. |
| **Riesgo residual** | Un empleado todavía puede interactuar con un phishing, pero una contraseña robada no debería ser suficiente para mantener acceso. |

**Nota de análisis:** el correo fue el canal inicial, pero el activo decisivo fue la identidad. Proteger únicamente el filtro antispam no cierra el camino de ataque.

---

## R2 · Acceso a cuentas de clientes mediante credential stuffing

| Campo | Valor |
|-------|-------|
| **Descripción** | Un atacante prueba credenciales filtradas de otros servicios contra las cuentas de clientes de FinTrack. |
| **Activos** | A1, A2 y A3. |
| **Propiedad violada (CID)** | Confidencialidad e integridad. |
| **Probabilidad** | **Media** — el acceso está expuesto a Internet y el ataque puede automatizarse, pero no existe evidencia de un incidente confirmado en FinTrack. |
| **Impacto** | **Alto** — una cuenta comprometida puede exponer datos financieros y permitir operaciones no autorizadas. |
| **Nivel** | **Alto** |
| **Escenario concreto** | Un bot prueba pares de usuario y contraseña filtrados, obtiene acceso a varias cuentas y consulta movimientos o intenta programar transferencias. |
| **Control** | **C2 — Protección de autenticación de clientes:** límites de intentos, detección de automatización, verificación de credenciales filtradas, MFA adaptativo y alertas de inicio de sesión. |
| **Riesgo residual** | Las cuentas con credenciales reutilizadas seguirán siendo objetivo, pero la automatización y el uso posterior deberían ser detectados o bloqueados. |

**Nota de análisis:** exigir contraseñas complejas no resuelve credenciales válidas que ya fueron filtradas; se necesita detectar comportamiento automatizado y riesgo de sesión.

---

## R3 · Compromiso de proveedores o integraciones externas

| Campo | Valor |
|-------|-------|
| **Descripción** | Un proveedor comprometido o una credencial de integración expuesta permite acceder indirectamente a datos, infraestructura o transferencias. |
| **Activos** | A5 directamente; A1, A2 y A3 como impacto. |
| **Propiedad violada (CID)** | Confidencialidad, integridad y disponibilidad. |
| **Probabilidad** | **Media** — FinTrack depende de correo, nube y una API bancaria, pero no existe evidencia de un compromiso actual de esos terceros. |
| **Impacto** | **Alto** — una integración con permisos amplios puede afectar operaciones financieras o dejar indisponible un servicio crítico. |
| **Nivel** | **Alto** |
| **Escenario concreto** | Una clave de API bancaria queda expuesta o un proveedor de correo es comprometido, permitiendo al atacante utilizar el acceso heredado hacia servicios de FinTrack. |
| **Control** | **C3 — Gestión de terceros y secretos:** revisión mínima de proveedores, permisos limitados, rotación de secretos, inventario de integraciones y procedimiento de revocación. |
| **Riesgo residual** | FinTrack no controla completamente la seguridad del proveedor, pero puede limitar el alcance y la duración del acceso concedido. |

**Nota de análisis:** contratar un servicio externo no transfiere el impacto del incidente; FinTrack conserva la responsabilidad de controlar qué acceso entrega.

---

## R4 · Abuso o autorización incorrecta en la API pública

| Campo | Valor |
|-------|-------|
| **Descripción** | Un atacante explota validaciones o autorizaciones deficientes para consultar datos ajenos, automatizar solicitudes o ejecutar funciones no permitidas. |
| **Activos** | A1, A2 y A3. |
| **Propiedad violada (CID)** | Confidencialidad, integridad y disponibilidad. |
| **Probabilidad** | **Media** — la API está expuesta a Internet y es un punto central de acceso, aunque no se ha confirmado una vulnerabilidad concreta. |
| **Impacto** | **Alto** — una falla de autorización puede escalar a exposición masiva de datos o manipulación de operaciones. |
| **Nivel** | **Alto** |
| **Escenario concreto** | Un usuario autenticado modifica un identificador en una solicitud y accede a movimientos de otro cliente, o automatiza consultas hasta degradar el servicio. |
| **Control** | **C4 — Seguridad de API:** autorización por objeto y función, validación de entradas, límites de solicitudes, inventario de endpoints, registros y pruebas de seguridad en cambios críticos. |
| **Riesgo residual** | Pueden persistir errores de lógica no detectados; las revisiones y el monitoreo reducen su exposición y tiempo de permanencia. |

**Nota de análisis:** un firewall tradicional no puede determinar por sí solo si un usuario autenticado está autorizado para consultar un objeto específico.

---

## R5 · Interrupción por malware o ransomware

| Campo | Valor |
|-------|-------|
| **Descripción** | Malware en un equipo o servicio cifra información, roba sesiones o interrumpe la operación de la plataforma. |
| **Activos** | A3 y A4 directamente; A1 y A2 durante la propagación o recuperación. |
| **Propiedad violada (CID)** | Disponibilidad e integridad; potencialmente confidencialidad. |
| **Probabilidad** | **Media** — el correo y los equipos de empleados ofrecen vectores realistas, pero no existe evidencia de infección activa. |
| **Impacto** | **Alto** — una interrupción puede impedir operaciones de 28.000 clientes y exigir restauración urgente. |
| **Nivel** | **Alto** |
| **Escenario concreto** | Un archivo malicioso ejecutado por un empleado roba sesiones o cifra recursos compartidos, afectando soporte, desarrollo y acceso a servicios. |
| **Control** | **C5 — Protección, respaldo y recuperación:** endurecimiento de equipos, protección de endpoints, copias aisladas, pruebas de restauración y segmentación lógica. |
| **Riesgo residual** | Ningún control elimina todo malware; el objetivo es limitar la propagación y recuperar funciones críticas sin pagar un rescate. |

**Nota de análisis:** las copias de seguridad reducen el impacto, pero no evitan el acceso inicial ni la posible extracción de información.

---

## R6 · Detección tardía y respuesta insuficiente

| Campo | Valor |
|-------|-------|
| **Descripción** | Un incidente permanece activo porque los registros no están centralizados, no existen alertas y la respuesta depende de decisiones improvisadas. |
| **Activos** | A1–A5 de forma transversal. |
| **Propiedad violada (CID)** | Confidencialidad, integridad y disponibilidad. |
| **Probabilidad** | **Alta** — el incidente permaneció seis días y fue detectado por un compañero, no por un mecanismo técnico. |
| **Impacto** | **Alto** — aumenta el tiempo de permanencia, dificulta determinar el alcance y retrasa la contención. |
| **Nivel** | **Crítico** |
| **Escenario concreto** | Se produce un acceso desde una ubicación y dispositivo anómalos, se crea una regla de reenvío y no se genera ninguna alerta hasta varios días después. |
| **Control** | **C6 — Monitoreo y respuesta:** centralización de logs, alertas de identidad y correo, retención mínima, responsables definidos, plan y playbook de phishing. |
| **Riesgo residual** | Algunas alertas producirán falsos positivos, pero el equipo dispondrá de evidencia y criterios para investigar y contener. |

**Nota de análisis:** R6 no es un vector de entrada; es un multiplicador que aumenta el impacto de todos los demás riesgos.

---

## Argumento de priorización

1. **Primera prioridad: R1 y R6.** Ambos ya se materializaron. MFA, acceso condicional, alertas básicas y un playbook ofrecen una reducción inmediata con un costo compatible con un equipo de cuatro personas.
2. **Segunda prioridad: R2 y R4.** La autenticación de clientes y la API están expuestas a Internet. Un ataque automatizado puede crecer rápidamente y afectar datos o transferencias.
3. **Tercera prioridad: R3 y R5.** Tienen impacto alto, pero requieren más coordinación operativa. Deben tratarse con controles mínimos sostenibles: permisos limitados, rotación de secretos, protección de endpoints y restauraciones probadas.

El orden no significa aceptar R3 o R5. Significa cerrar primero el camino que ya fue explotado y crear capacidad de detección antes de desplegar controles más costosos.

---

## Riesgos evaluados y descartados

| Riesgo considerado | Por qué no entra al registro |
|--------------------|------------------------------|
| Ataque estatal avanzado | No corresponde al perfil de amenaza más probable de una fintech de este tamaño y exigiría inversiones desproporcionadas frente a los riesgos observados. |
| Sabotaje físico del centro de datos | La infraestructura está en nube pública; el riesgo físico se gestiona principalmente mediante la evaluación contractual y operativa del proveedor. |
| DDoS volumétrico como riesgo separado | Se mantiene como escenario de disponibilidad dentro de R3, R4 y la continuidad operativa, pero no desplaza a riesgos ya materializados. |
| Fraude interno como riesgo independiente | Se tratará inicialmente mediante mínimo privilegio, segregación de funciones y monitoreo incluidos en C1 y C6. Se separará si aparecen indicadores específicos. |
| Vulnerabilidad desconocida de alta complejidad | Es posible, pero tiene menor probabilidad que phishing, credential stuffing, abuso de API y configuraciones inseguras. |

---

## Trazabilidad hacia la siguiente sección

| Riesgo | Control que debe desarrollarse en `04-security-controls/` |
|--------|----------------------------------------------------------|
| R1 | C1 — Protección de identidad y acceso |
| R2 | C2 — Protección de autenticación de clientes |
| R3 | C3 — Gestión de terceros y secretos |
| R4 | C4 — Seguridad de API |
| R5 | C5 — Protección, respaldo y recuperación |
| R6 | C6 — Monitoreo y respuesta a incidentes |

---
