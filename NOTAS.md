# Notas de implementación

El README original exige React y PHP/Laravel. La tecnología de los planes se traduce; se preservan negocio, contrato, datos, arquitectura hexagonal y ADR. El spec original no se modifica.

- Laravel queda en adaptadores y composición; dominio y aplicación no importan framework ni ORM.
- PostgreSQL 16, esquema library; seis tablas de negocio sin columnas de auditoría ni DEFAULT. public.migrations es metadato técnico de Laravel.
- JWT HS256 de ocho horas y BCrypt factor 12 detrás de puertos. Admin provisionado desde entorno.
- ADR-002: se prevé usar xmin como testigo de versión PostgreSQL para no añadir columnas al modelo físico. Préstamos y concurrencia aún pendientes.
- Sembrador por API, nunca SQL directo, como exige tasks T-21; la sugerencia de SQL en la captura no reemplaza ese requisito.
- Se conservarán avances parciales con evidencia y commits Conventional Commits en inglés. No se alterará la fecha de commits para aparentar cumplimiento del plazo.
