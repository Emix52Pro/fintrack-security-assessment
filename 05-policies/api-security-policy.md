# Política de seguridad de API y cambios

**Mitiga:** R4 — Abuso o autorización incorrecta en la API pública  
**Responsable:** Responsable de Desarrollo  
**Aplica a:** APIs, backend, aplicaciones web y móvil, y cambios que procesen datos o transferencias  
**Última revisión:** 2026-07-18

## Propósito

Impedir que un usuario autenticado consulte datos ajenos, ejecute funciones no autorizadas o abuse de endpoints expuestos.

## Regla

1. Validar en el servidor la identidad, el rol, la propiedad del recurso y la autorización de cada operación sensible.
2. No aceptar identificadores, montos, roles o permisos enviados por el cliente sin validación independiente.
3. Aplicar límites de solicitudes, validación de entradas y registros en todos los endpoints públicos.
4. Exigir revisión de código por otra persona para cambios en autenticación, autorización, transferencias o datos financieros.
5. Incluir pruebas automáticas que intenten acceder a objetos de otro usuario y ejecutar funciones sin permiso.
6. Mantener un inventario de endpoints, propietarios, datos procesados y nivel de criticidad.
7. Retirar o bloquear versiones y endpoints sin uso dentro de un plazo definido.
8. Registrar despliegues y conservar un procedimiento de reversión para cambios críticos.

## Excepciones

Un cambio urgente puede desplegarse sin revisión previa únicamente para contener un incidente activo. El responsable de Desarrollo debe registrar la razón, el riesgo aceptado y el plan de reversión, y completar la revisión y pruebas dentro de las siguientes 24 horas.

## Verificación

Desarrollo revisa en cada despliegue la evidencia de revisión, pruebas y reversión. Mensualmente verifica el inventario de endpoints, errores de autorización, límites de solicitudes y rutas sin propietario. Trimestralmente ejecuta una prueba de acceso a un recurso ajeno y documenta el resultado.
