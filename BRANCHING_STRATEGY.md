# Organizacion de ramas - Manager Library

Este documento define como se organizaran las ramas de trabajo para desarrollar Manager Library siguiendo SDD. La fuente de verdad sigue siendo el spec de `test-manager-library-3145555-docs`; este repositorio documenta la estrategia de entrega y evidencias.

## Principios de trabajo

- La rama `dev` es la base de integracion, pero no se trabaja ni se sube evidencia directamente desde ella.
- Cada cambio nace en una rama hija con una nomenclatura clara.
- Los commits deben escribirse en ingles.
- Cada rama debe dejar evidencia verificable de la historia o tarea que resuelve.
- No se inventan reglas de negocio: se implementa lo que aparece en `constitution.md`, `spec.md`, `api-contract.md`, `data-model.md` y `tasks.md`.
- `infra` solo levanta servicios vacios; el esquema de base de datos pertenece a las migraciones del backend.

## Nomenclatura

| Repositorio | Tipo de rama | Ejemplo |
|---|---|---|
| `test-manager-library-3145555-docs-` | `feature/<scope>` | `feature/branch-organization` |
| `test-manager-library-3145555-api` | `HU-XX-<short-name>` | `HU-01-health-check` |
| `test-manager-library-3145555-app` | `HU-XX-<short-name>` | `HU-01-health-check` |
| `test-manager-library-3145555-infra` | `HU-XX-<short-name>` | `HU-01-health-check` |
| `test-manager-library-3145555-page` | `HU-XX-<short-name>` | `HU-01-health-check` |
| `test-manager-library-3145555-tool-` | `HU-XX-<short-name>` | `HU-01-health-check` |

## Primer corte de trabajo

| Repositorio | Rama | Objetivo | Evidencia esperada |
|---|---|---|---|
| `docs-` | `feature/branch-organization` | Documentar estrategia de ramas y traduccion del spec a Laravel/React | Este archivo versionado |
| `infra` | `HU-01-health-check` | Preparar contenedores base y PostgreSQL vacio | `docker compose` sin `CREATE TABLE` |
| `api` | `HU-01-health-check` | Preparar Laravel y exponer `/health` | `GET /health` responde `{ "status": "ok" }` |
| `app` | `HU-01-health-check` | Reservar la integracion inicial del frontend con salud de API | README con alcance de HU-01 |
| `page` | `HU-01-health-check` | Reservar evidencia inicial del sitio publico | README con alcance de HU-01 |
| `tool-` | `HU-01-health-check` | Reservar utilidades futuras que usaran la API | README con alcance de HU-01 |

## Orden recomendado por SDD

1. Leer y respetar `constitution.md`, `spec.md` y `plan.md`.
2. Crear el arranque basico: backend Laravel, configuracion y ruta publica `/health`.
3. Crear infraestructura con PostgreSQL vacio, volumen persistente y red compartida.
4. Crear migraciones en el backend para las seis tablas y las cinco categorias iniciales.
5. Implementar dominio y casos de uso por HU.
6. Conectar adaptadores reales: PostgreSQL, autenticacion, portadas y API HTTP.
7. Construir React y el sembrador usando el contrato HTTP.

## Traduccion del plan tecnico

| Spec de referencia | Entrega real |
|---|---|
| Python/FastAPI o .NET/ASP.NET | PHP con Laravel |
| Alembic o EF Core migrations | Migraciones de Laravel |
| pytest o xUnit | PHPUnit o Pest |
| Puerto `Clock` | Servicio/contrato de reloj en la capa de aplicacion |
| Puerto `PasswordHasher` | Adaptador sobre `Hash` de Laravel |
| JWT HS256 | Autenticacion por token JWT con vigencia de 8 horas |
| PostgreSQL 16 | PostgreSQL 16 en `infra`, sin tablas iniciales |

## Commits sugeridos

- `Document branch organization strategy`
- `Add health check Laravel skeleton`
- `Add empty PostgreSQL infrastructure`
- `Document HU-01 frontend scope`
- `Document HU-01 public page scope`
- `Document HU-01 tool scope`
