# Evaluación de Seguridad — FinTrack Solutions

> Evaluación integral de seguridad para una fintech ficticia, desarrollada como proyecto de portafolio profesional.

## Sobre este proyecto

FinTrack Solutions es una fintech ficticia de gestión de finanzas personales con aproximadamente 28.000 clientes y 45 empleados. Este repositorio documenta una evaluación de seguridad completa, desde el contexto de negocio y la arquitectura hasta el análisis de riesgos, los controles, las políticas, la respuesta a incidentes y las recomendaciones finales.

El proyecto parte de un incidente de phishing contra una cuenta del área de Finanzas y utiliza ese caso para identificar debilidades reales, priorizar controles sostenibles y demostrar trazabilidad entre riesgos, decisiones y acciones correctivas.

## Hallazgo central

> **El perímetro de FinTrack no es únicamente su red: es la identidad.**

Una contraseña comprometida permitió acceso desde una ubicación y dispositivo anómalos, creación de una regla de reenvío y persistencia durante casi seis días. La evaluación concluye que FinTrack debe priorizar MFA, acceso condicional, mínimo privilegio, alertas de identidad y una respuesta operativa documentada.

## Alcance

La evaluación incluye:

- Identificación de activos críticos.
- Arquitectura y superficie de ataque.
- Modelo de amenazas.
- Registro de seis riesgos priorizados.
- Controles C1–C6 con alternativas y descartes.
- Políticas mínimas viables.
- Plan de respuesta y playbook de phishing.
- Postmortem del incidente.
- Hoja de ruta de implementación.

No incluye pruebas de penetración, certificación ISO 27001 ni migración completa de infraestructura.

## Estructura del repositorio

| Sección | Contenido |
|---------|-----------|
| [`01-business-case.md`](01-business-case.md) | Cliente, activos, alcance y restricciones |
| [`02-architecture/`](02-architecture/) | Arquitectura, zonas de confianza y superficie de ataque |
| [`03-risk-analysis/`](03-risk-analysis/) | Modelo de amenazas y registro R1–R6 |
| [`04-security-controls/`](04-security-controls/) | Controles propuestos C1–C6 |
| [`05-policies/`](05-policies/) | Políticas mínimas vinculadas a los riesgos |
| [`06-incident-response/`](06-incident-response/) | Plan de respuesta y playbook de phishing |
| [`07-postmortem/`](07-postmortem/) | Postmortem del incidente simulado |
| [`08-recommendations.md`](08-recommendations.md) | Recomendaciones y hoja de ruta final |

## Riesgos principales

| ID | Riesgo | Nivel |
|----|--------|-------|
| R1 | Compromiso de identidad interna mediante phishing | Crítico |
| R2 | Acceso a cuentas mediante credential stuffing | Alto |
| R3 | Compromiso de proveedores o integraciones | Alto |
| R4 | Abuso o autorización incorrecta en la API | Alto |
| R5 | Interrupción por malware o ransomware | Alto |
| R6 | Detección tardía y respuesta insuficiente | Crítico |

## Trazabilidad

Cada recomendación se relaciona con un riesgo y un control específico:

```text
Activo A# → amenaza → riesgo R# → control C# → política → respuesta → recomendación
```

Esta trazabilidad evita controles genéricos y permite justificar cada decisión según el impacto, la probabilidad, el costo y la capacidad operativa de FinTrack.

## Prioridades recomendadas

1. Proteger las identidades internas y administrativas.
2. Detectar accesos anómalos en minutos.
3. Reforzar la autenticación de clientes y la API.
4. Limitar accesos de terceros y secretos.
5. Probar copias de seguridad y recuperación.
6. Medir el funcionamiento de los controles mediante simulacros.

## Criterio profesional

No se recomienda implementar inicialmente un SIEM empresarial, migrar toda la infraestructura o buscar una certificación formal. Para una empresa de 45 empleados y cuatro personas en TI, esos esfuerzos ofrecen menos valor inmediato que MFA, acceso condicional, alertas específicas, mínimo privilegio y procedimientos de respuesta verificables.

## Resultado esperado

Al finalizar la hoja de ruta, FinTrack debe poder:

- Identificar sus seis riesgos principales.
- Demostrar qué control mitiga cada riesgo.
- Detectar un acceso sospechoso sin depender de una observación humana.
- Contener una cuenta comprometida en menos de 30 minutos.
- Recuperar servicios críticos desde copias verificadas.
- Documentar y mejorar cada incidente mediante un postmortem.

## Autor

**Gabriel Emilio García Mazón**  
[LinkedIn](https://www.linkedin.com/in/gabriel-garcía-a848b1306) · [GitHub](https://github.com/Emix52Pro)
