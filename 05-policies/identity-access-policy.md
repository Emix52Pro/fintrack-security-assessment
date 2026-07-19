# Política de identidad y acceso

**Mitiga:** R1 — Compromiso de identidad interna mediante phishing; R2 — Acceso a cuentas de clientes mediante credential stuffing  
**Responsable:** Responsable de Infraestructura de TI  
**Aplica a:** empleados, administradores, cuentas de servicio y clientes de FinTrack  
**Última revisión:** 2026-07-18

## Propósito

Evitar que una contraseña robada sea suficiente para acceder a sistemas, correos, datos financieros o funciones sensibles.

## Regla

1. Activar MFA en todas las cuentas internas; Finanzas, TI y administradores deben usar un factor resistente al phishing cuando esté disponible.
2. Separar las cuentas administrativas de las cuentas de uso cotidiano y prohibir cuentas compartidas.
3. Asignar permisos por función y retirar accesos que no sean necesarios para el puesto.
4. Revisar los accesos de empleados cada trimestre y al cambiar de cargo o salir de la empresa.
5. Revocar sesiones y cambiar credenciales inmediatamente ante phishing, acceso anómalo o pérdida de dispositivo.
6. Aplicar límites de intentos, alertas de nuevo dispositivo y verificación adicional en transferencias o cambios sensibles de clientes.
7. Bloquear contraseñas conocidas como filtradas y exigir cambio cuando exista evidencia de exposición.

## Excepciones

Toda excepción debe ser solicitada por el responsable del área, aprobada por Infraestructura de TI y registrada con motivo, alcance, control compensatorio y fecha de vencimiento. Las cuentas administrativas y de Finanzas no pueden quedar sin MFA; si el segundo factor falla, TI debe aplicar un mecanismo temporal de recuperación y revocar las sesiones anteriores.

## Verificación

Infraestructura de TI revisa mensualmente el porcentaje de cuentas con MFA, cuentas sin propietario, privilegios administrativos, excepciones vigentes y accesos anómalos. Cada trimestre conserva evidencia de la revisión de permisos y de una prueba de bloqueo de acceso sin segundo factor.
