# Política de terceros y secretos

**Mitiga:** R3 — Compromiso de proveedores o integraciones externas  
**Responsable:** Responsable de Infraestructura de TI  
**Aplica a:** proveedores de nube, correo, banca, APIs y cualquier integración con acceso a datos o sistemas de FinTrack  
**Última revisión:** 2026-07-18

## Propósito

Limitar el impacto de un proveedor comprometido o de una clave, token o cuenta de servicio expuesta.

## Regla

1. Registrar cada proveedor e integración con responsable, finalidad, datos accesibles, permisos, credenciales y fecha de revisión.
2. Conceder únicamente los permisos necesarios y utilizar una cuenta de servicio distinta por integración.
3. Guardar claves y tokens en el gestor de secretos del proveedor de nube; no incluirlos en código, repositorios, correos o archivos compartidos.
4. Rotar credenciales críticas al menos cada 90 días y de inmediato ante exposición, cambio de proveedor o incidente.
5. Evaluar antes de contratar un tercero sus prácticas de autenticación, registros, notificación de incidentes, continuidad y eliminación de datos.
6. Documentar cómo revocar cada integración sin afectar innecesariamente otros servicios.
7. Revisar anualmente los proveedores y eliminar integraciones sin uso o sin responsable.

## Excepciones

Si una aplicación antigua no admite el gestor de secretos o la rotación automática, Desarrollo debe documentar el motivo, cifrar la credencial, limitar sus permisos y definir una fecha de corrección. Infraestructura aprueba la excepción y la revisa mensualmente hasta su cierre.

## Verificación

Infraestructura mantiene el inventario actualizado y revisa mensualmente secretos vencidos, credenciales sin rotación, permisos excesivos e integraciones sin propietario. Cada trimestre se prueba la revocación de al menos una credencial no productiva y se conserva la evidencia.
