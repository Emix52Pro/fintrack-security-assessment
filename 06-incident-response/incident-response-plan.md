# 06 — Plan de Respuesta a Incidentes

**Decisión que permite tomar este documento:** definir quién actúa, qué se hace y cuándo durante los primeros 60 minutos de un incidente en FinTrack.

---

## Objetivo

Contener incidentes con rapidez, preservar evidencia, reducir el impacto sobre clientes y operaciones, y evitar respuestas improvisadas.

---

## Roles

| Rol | Responsabilidad | Quién |
|-----|-----------------|-------|
| **Coordinador del incidente** | Declara el incidente, asigna prioridades, autoriza medidas de contención y comunica a Dirección. | Responsable de Infraestructura |
| **Analista técnico** | Revisa logs, identidad, correo, nube, endpoints y determina alcance e indicadores de compromiso. | Desarrollador 1 |
| **Contención y recuperación** | Bloquea cuentas, revoca sesiones, aísla equipos, restaura servicios y valida la recuperación. | Desarrollador 2 |
| **Registro y soporte** | Recibe reportes, conserva evidencias, documenta la cronología y comunica instrucciones a usuarios. | Soporte TI |
| **Responsable de negocio** | Evalúa impacto financiero, operativo, legal y de clientes. | Dirección o responsable de Finanzas |
| **Apoyo externo** | Asiste cuando el incidente supera la capacidad interna. | Proveedor de nube, correo, banco o asesor externo |

Una misma persona puede asumir más de un rol, pero el coordinador debe quedar claramente identificado desde el inicio.

---

## Clasificación inicial

| Severidad | Criterio | Ejemplo |
|-----------|----------|---------|
| **Crítica** | Transferencias no autorizadas, exposición confirmada de datos financieros, compromiso administrativo o interrupción general. | Uso indebido del motor de transferencias. |
| **Alta** | Cuenta interna comprometida, malware activo, regla de reenvío externo o acceso desde una ubicación imposible. | Incidente similar al de `a.torres`. |
| **Media** | Actividad anómala sin evidencia confirmada de compromiso. | Múltiples intentos fallidos desde una IP desconocida. |
| **Baja** | Evento aislado sin impacto ni continuidad. | Correo sospechoso no abierto. |

Los incidentes críticos y altos activan este plan de inmediato.

---

## Primeros 60 minutos

| Tiempo | Acción | Responsable |
|--------|--------|-------------|
| **0–10 min** | Confirmar el reporte, abrir el registro del incidente, clasificar severidad y preservar el mensaje o alerta original. | Soporte TI + Coordinador |
| **10–20 min** | Revocar sesiones, bloquear o limitar la cuenta afectada, cambiar credenciales y detener reglas o tokens sospechosos. | Contención |
| **20–35 min** | Revisar accesos recientes, IP, ubicación, dispositivo, correo, privilegios, API y actividad relacionada. | Analista técnico |
| **35–45 min** | Determinar alcance: usuarios, sistemas, datos, transferencias, terceros y posibles cuentas secundarias. | Analista + Coordinador |
| **45–60 min** | Informar a Dirección, definir siguientes acciones, conservar evidencia y asignar responsables para erradicación y recuperación. | Coordinador |

---

## Fases

### 1. Detección

1. Recibir alertas técnicas, reportes de empleados, clientes o proveedores.
2. Registrar fecha, hora, usuario, sistema, fuente y descripción inicial.
3. Validar la alerta con al menos una fuente adicional cuando sea posible.
4. Clasificar severidad según el impacto potencial y los activos afectados.
5. Activar el playbook correspondiente.

**Evidencia mínima:** correo original, encabezados, capturas, logs, IP, usuario, dispositivo, reglas de correo y acciones observadas.

---

### 2. Contención

1. Revocar sesiones activas y tokens de la cuenta comprometida.
2. Bloquear temporalmente la cuenta si el acceso continúa.
3. Restablecer credenciales mediante un canal seguro.
4. Eliminar reglas de reenvío, aplicaciones autorizadas o claves sospechosas.
5. Aislar el equipo si existe riesgo de malware.
6. Bloquear IP, dispositivo o integración cuando el impacto sea controlable.
7. Preservar los logs antes de realizar cambios irreversibles.

La contención debe detener el acceso sin destruir evidencia ni interrumpir servicios innecesariamente.

---

### 3. Erradicación

1. Identificar y eliminar el mecanismo de persistencia.
2. Revisar permisos, cuentas, tokens, reglas, claves y cambios realizados.
3. Corregir configuraciones débiles que permitieron el incidente.
4. Actualizar o reinstalar equipos comprometidos cuando corresponda.
5. Rotar secretos o credenciales vinculadas.
6. Buscar los mismos indicadores en otros usuarios y sistemas.

---

### 4. Recuperación

1. Restaurar cuentas y servicios solo después de validar que el acceso malicioso terminó.
2. Aplicar MFA y controles adicionales antes de devolver el acceso.
3. Confirmar que correo, API, datos y transferencias funcionan normalmente.
4. Monitorear de forma reforzada durante al menos 72 horas.
5. Comunicar el cierre operativo a Dirección y responsables afectados.
6. Mantener abierto el incidente si quedan dudas sobre datos o transacciones.

---

### 5. Lecciones aprendidas

1. Elaborar el postmortem dentro de los cinco días hábiles siguientes.
2. Reconstruir la cronología completa.
3. Identificar qué funcionó, qué falló y qué evidencia faltó.
4. Definir acciones correctivas con responsable, prioridad y fecha.
5. Actualizar alertas, controles, políticas y playbooks.
6. Comunicar aprendizajes sin culpar a la persona que reportó el incidente.

---

## Cómo escalar

| Condición | Escalamiento | Canal |
|-----------|--------------|-------|
| Transferencia no autorizada o posible fraude | Dirección, Finanzas y proveedor bancario | Llamada inmediata + correo de seguimiento |
| Exposición confirmada o probable de datos personales | Dirección y asesoría legal | Llamada inmediata + registro escrito |
| Compromiso de correo o nube fuera de capacidad interna | Proveedor correspondiente | Canal de soporte de emergencia |
| Malware extendido o recuperación incierta | Especialista externo o MDR | Teléfono y ticket prioritario |
| Interrupción que afecta a clientes | Dirección y responsable de comunicación | Reunión urgente y mensaje aprobado |
| Incidente crítico sin contención en 30 minutos | Dirección ejecutiva | Llamada directa |

No se debe comunicar públicamente un incidente sin autorización de Dirección y revisión legal.

---

## Contactos

| Contacto | Cuándo avisar | Información que recibe |
|----------|---------------|------------------------|
| **Dirección** | Incidente alto o crítico | Impacto, alcance, medidas y decisiones necesarias |
| **Finanzas** | Riesgo de fraude o transferencias | Operaciones afectadas y acciones de bloqueo |
| **Responsable de datos o asesor legal** | Posible exposición de información personal | Tipo de datos, alcance y evidencia disponible |
| **Proveedor de correo** | Compromiso de cuenta, reglas o sesiones | Usuario, hora, IP y acciones requeridas |
| **Proveedor de nube** | Acceso, logs o recursos comprometidos | Recursos, indicadores y prioridad |
| **Proveedor bancario** | Transferencias o credenciales de integración afectadas | Operaciones, claves y solicitud de contención |
| **Clientes afectados** | Solo con aprobación de Dirección y Legal | Hechos confirmados, impacto y acciones recomendadas |

Los nombres, teléfonos y correos reales deben mantenerse en un directorio interno, no en el repositorio público.

---

## Evidencia y registro

Cada incidente debe conservar:

- Identificador único.
- Fecha y hora de detección.
- Persona que reportó.
- Sistemas, cuentas y activos afectados.
- Logs y archivos relevantes.
- Acciones ejecutadas y responsables.
- Decisiones de escalamiento.
- Impacto confirmado y potencial.
- Estado final y acciones correctivas.

---

## Métricas mínimas

| Métrica | Objetivo inicial |
|---------|------------------|
| Tiempo hasta reconocer el incidente | Menos de 15 minutos |
| Tiempo hasta contención inicial | Menos de 30 minutos |
| Porcentaje de incidentes con cronología completa | 100 % |
| Acciones correctivas cerradas en plazo | 90 % |
| Simulacros realizados | Al menos uno por trimestre |

---

## Relación con riesgos y controles

| Riesgo | Aplicación del plan |
|--------|---------------------|
| R1 | Contención de cuentas comprometidas y phishing |
| R3 | Coordinación con proveedores e integraciones |
| R5 | Aislamiento, respaldo y recuperación |
| R6 | Roles, alertas, escalamiento y documentación |

---
