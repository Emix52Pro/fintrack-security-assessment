# 05 — Políticas mínimas viables

Cada política existe porque un riesgo la exige. Una política por archivo.

## Mapeo política → riesgo

| Política | Archivo | Mitiga |
|----------|---------|--------|
| Política de identidad y acceso | `identity-access-policy.md` | R1, R2 |
| Política de terceros y secretos | `third-party-secrets-policy.md` | R3 |
| Política de seguridad de API y cambios | `api-security-policy.md` | R4 |
| Política de continuidad, monitoreo y respuesta | `continuity-monitoring-policy.md` | R5, R6 |

## Criterio de aplicación

Las políticas se diseñaron para una empresa de 45 empleados, cuatro integrantes de TI y sin equipo dedicado de seguridad. Cada regla debe ser verificable con evidencia y mantenerse con herramientas disponibles en la nube actual.

## Lo que NO se escribe

| Política descartada | Razón |
|---------------------|-------|
| Política independiente de teletrabajo | Sus riesgos principales ya se cubren mediante identidad, dispositivos, mínimo privilegio y monitoreo. |
| Política extensa de clasificación documental | FinTrack necesita primero identificar y proteger datos financieros críticos; un esquema corporativo complejo sería prematuro. |
| Política de certificación ISO 27001 | La certificación no es un control operativo. Primero deben funcionar los controles, registros y responsabilidades básicas. |
| Política separada contra actores estatales | No responde a uno de los seis riesgos priorizados y exigiría medidas desproporcionadas para FinTrack. |
| Política de uso aceptable extensa | No reduce por sí sola los riesgos críticos. Sus reglas esenciales se integran en identidad, dispositivos y respuesta. |
