# 04 — Controles de Seguridad Propuestos

**Decisión que permite tomar este documento:** seleccionar qué controles debe implementar FinTrack, en qué orden y con qué nivel de inversión para reducir sus seis riesgos principales.

> Regla: cada control cita el riesgo R# que mitiga. Por cada control, las
> opciones consideradas incluyen su ventaja y su limitación. La recomendación
> se ajusta a una empresa de 45 personas, cuatro integrantes de TI y sin equipo
> dedicado de seguridad.

---

## C1 · Protección de identidad y acceso — mitiga R1

**Objetivo:** impedir que una contraseña robada mediante phishing sea suficiente para acceder al correo o a sistemas internos.

| Opción | Pro | Contra |
|--------|-----|--------|
| **A. MFA con aplicación autenticadora, acceso condicional y mínimo privilegio** | Bajo costo, rápida implementación y reduce directamente el uso de credenciales robadas. | Requiere configurar excepciones, recuperación de cuentas y revisar alertas de acceso. |
| **B. Llaves físicas FIDO2 para todos los empleados** | Alta resistencia al phishing y menor dependencia de códigos o notificaciones. | Mayor costo, logística de entrega, reposición y soporte para 45 usuarios. |

> **Recomendación:** aplicar la opción A a toda la empresa y usar llaves FIDO2 primero en Finanzas, TI y cuentas administrativas. Separar las cuentas administrativas de las cuentas de uso diario, revocar sesiones sospechosas y bloquear accesos desde dispositivos o ubicaciones de alto riesgo.  
> **Cuándo:** MFA y revocación de sesiones esta semana; acceso condicional y revisión de privilegios este mes.

**Resultado esperado:** una contraseña obtenida por phishing no permite mantener una sesión válida sin una segunda verificación.

---

## C2 · Protección de autenticación de clientes — mitiga R2

**Objetivo:** reducir intentos automatizados de credential stuffing y detectar accesos anómalos a cuentas de clientes.

| Opción | Pro | Contra |
|--------|-----|--------|
| **A. Límite de intentos, retraso progresivo, CAPTCHA y alertas de inicio de sesión** | Económico, reduce automatización básica y puede implementarse en la aplicación actual. | Puede afectar a usuarios legítimos y no detiene credenciales válidas usadas lentamente. |
| **B. MFA adaptativo, detección de credenciales filtradas y análisis de riesgo de sesión** | Protege mejor las cuentas de alto riesgo y reduce fricción para usuarios normales. | Requiere integración adicional, reglas de riesgo y soporte al cliente. |

> **Recomendación:** implementar primero la opción A y añadir MFA adaptativo para transferencias, cambios de datos sensibles y accesos anómalos. Bloquear contraseñas conocidas como filtradas y notificar al cliente cuando se detecte un nuevo dispositivo.  
> **Cuándo:** límites y alertas este mes; MFA adaptativo este trimestre.

**Resultado esperado:** los intentos automatizados son bloqueados y las operaciones sensibles requieren verificación adicional.

---

## C3 · Gestión de terceros y secretos — mitiga R3

**Objetivo:** limitar el impacto de un proveedor comprometido o de una credencial de integración expuesta.

| Opción | Pro | Contra |
|--------|-----|--------|
| **A. Inventario manual de proveedores, permisos mínimos y rotación periódica de claves** | Bajo costo y viable con el equipo actual. | Depende de disciplina operativa y puede generar errores u omisiones. |
| **B. Gestor centralizado de secretos con rotación automática y cuentas de servicio separadas** | Reduce secretos expuestos y facilita revocación y auditoría. | Requiere configuración inicial y adaptación de aplicaciones existentes. |

> **Recomendación:** crear de inmediato un inventario de integraciones, responsables, permisos y fechas de rotación. Durante el trimestre, migrar claves y tokens al gestor de secretos del proveedor de nube, usando cuentas de servicio con permisos mínimos y credenciales independientes por integración.  
> **Cuándo:** inventario y revisión de permisos este mes; gestor de secretos y rotación automatizada este trimestre.

**Resultado esperado:** una credencial comprometida tiene alcance y vigencia limitados y puede revocarse sin afectar todas las integraciones.

---

## C4 · Seguridad de la API pública — mitiga R4

**Objetivo:** impedir accesos a datos u operaciones que un usuario autenticado no está autorizado a ejecutar.

| Opción | Pro | Contra |
|--------|-----|--------|
| **A. Controles nativos en API Gateway: autenticación, límites, validación y registros** | Aprovecha la infraestructura existente, tiene menor costo y es operable por el equipo de desarrollo. | No detecta por sí solo errores de lógica de negocio o autorización por objeto. |
| **B. Plataforma especializada de seguridad de API** | Ofrece descubrimiento automático, análisis avanzado y detección de abuso. | Costo alto y mayor complejidad para el tamaño actual de FinTrack. |

> **Recomendación:** usar la opción A, complementada con autorización por objeto y función dentro del backend, validación estricta de entradas y pruebas automáticas para endpoints críticos. Toda solicitud de transferencia debe validar identidad, propiedad del recurso y permisos en el servidor.  
> **Cuándo:** inventario y límites este mes; pruebas de autorización y revisión de endpoints críticos este trimestre.

**Resultado esperado:** modificar un identificador o automatizar solicitudes no permite consultar datos ajenos ni ejecutar operaciones no autorizadas.

---

## C5 · Protección, respaldo y recuperación — mitiga R5

**Objetivo:** limitar la propagación de malware y recuperar servicios críticos sin depender del pago de un rescate.

| Opción | Pro | Contra |
|--------|-----|--------|
| **A. Protección de endpoints, parches, copias aisladas y pruebas de restauración** | Cubre las fallas más probables con costos controlados y herramientas disponibles en nube. | Requiere mantenimiento continuo y pruebas periódicas para comprobar que las copias funcionan. |
| **B. Servicio MDR/EDR administrado las 24 horas** | Mejora detección y respuesta especializada sin contratar un equipo interno completo. | Costo recurrente mayor y dependencia de un proveedor externo. |

> **Recomendación:** implementar la opción A como base: protección de endpoints, actualizaciones prioritarias, restricción de privilegios locales, copias aisladas y restauraciones trimestrales. Evaluar un servicio MDR solo si la carga de alertas supera la capacidad del equipo de TI.  
> **Cuándo:** validar copias y parches críticos este mes; protección de endpoints y prueba de restauración este trimestre.

**Resultado esperado:** una infección queda limitada y FinTrack puede restaurar sus funciones críticas dentro de un tiempo definido.

---

## C6 · Monitoreo y respuesta a incidentes — mitiga R6

**Objetivo:** detectar accesos anómalos y contener incidentes antes de que permanezcan activos durante varios días.

| Opción | Pro | Contra |
|--------|-----|--------|
| **A. Centralización de logs y alertas nativas de nube, identidad y correo** | Bajo costo, rápida implementación y suficiente para los escenarios prioritarios. | Requiere seleccionar pocas alertas útiles y asignar responsables para revisarlas. |
| **B. SIEM empresarial con SOC externo 24/7** | Mayor cobertura, correlación avanzada y vigilancia continua. | Costo y complejidad desproporcionados para una empresa de 45 empleados. |

> **Recomendación:** aplicar la opción A. Centralizar eventos de autenticación, correo, API, administración y nube; conservarlos por un periodo definido y crear alertas para ubicación imposible, dispositivo desconocido, reenvío externo, actividad nocturna, múltiples fallos y cambios de privilegios. Cada alerta debe tener responsable, severidad y acción inicial.  
> **Cuándo:** alertas críticas y responsables esta semana; centralización, retención y playbooks este mes.

**Resultado esperado:** un acceso similar al incidente de `a.torres` genera una alerta en minutos y activa un procedimiento de contención documentado.

---

## Resumen: qué se hace y cuándo

| Cuándo | Acciones | Riesgos que atacan |
|--------|----------|--------------------|
| **Esta semana** | Activar MFA en cuentas internas; revocar sesiones; proteger cuentas administrativas; crear alertas por accesos anómalos y reglas de reenvío; asignar responsables de respuesta. | R1, R6 |
| **Este mes** | Aplicar acceso condicional; revisar privilegios; limitar intentos de clientes; inventariar terceros y secretos; configurar límites y registros de API; validar copias de seguridad. | R1, R2, R3, R4, R5, R6 |
| **Este trimestre** | Implementar MFA adaptativo; migrar secretos al gestor de nube; automatizar pruebas de autorización; desplegar protección de endpoints; probar restauración; formalizar monitoreo y playbooks. | R2, R3, R4, R5, R6 |

---

## Verificación de los controles

| Control | Evidencia mínima de funcionamiento |
|---------|-----------------------------------|
| C1 | Intento de acceso con contraseña válida pero sin segundo factor bloqueado. |
| C2 | Simulación de múltiples intentos automatizados limitada y registrada. |
| C3 | Inventario completo y rotación comprobada de una credencial de integración. |
| C4 | Prueba de acceso a un recurso ajeno rechazada por el backend. |
| C5 | Restauración exitosa de un servicio o conjunto de datos desde una copia aislada. |
| C6 | Alerta de acceso anómalo recibida y atendida según el playbook. |

---

## Lo que deliberadamente NO recomendamos

| Descartado | Por qué |
|-----------|---------|
| **SIEM empresarial y SOC externo 24/7 en la primera fase** | El costo y la complejidad superan la capacidad actual. Primero deben centralizarse los logs y crear alertas específicas con herramientas nativas. |
| **Llaves físicas para los 45 empleados desde el primer día** | Son efectivas, pero conviene priorizarlas en Finanzas, TI y administradores mientras se despliega MFA de menor costo al resto. |
| **Plataforma especializada de seguridad de API** | FinTrack puede reducir primero el riesgo con controles nativos, autorización correcta, límites y pruebas automatizadas. |
| **Migración completa de infraestructura** | No es necesaria para cerrar los caminos de ataque prioritarios y consumiría recursos que deben destinarse a identidad, monitoreo y recuperación. |
| **Certificación ISO 27001 inmediata** | Antes de certificar, FinTrack debe implementar y operar controles básicos, políticas y evidencias de cumplimiento. |
| **Capacitación como único control contra phishing** | La formación ayuda, pero no sustituye MFA, acceso condicional, mínimo privilegio ni monitoreo técnico. |

---

## Trazabilidad

| Riesgo | Control principal | Resultado buscado |
|--------|-------------------|-------------------|
| R1 | C1 — Protección de identidad y acceso | Credenciales robadas insuficientes para ingresar. |
| R2 | C2 — Protección de autenticación de clientes | Ataques automatizados bloqueados o detectados. |
| R3 | C3 — Gestión de terceros y secretos | Acceso externo limitado y revocable. |
| R4 | C4 — Seguridad de la API pública | Datos y operaciones protegidos por autorización efectiva. |
| R5 | C5 — Protección, respaldo y recuperación | Propagación limitada y recuperación comprobada. |
| R6 | C6 — Monitoreo y respuesta a incidentes | Detección y contención en minutos, no en días. |

---

