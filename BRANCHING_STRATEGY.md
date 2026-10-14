# Organización de ramas — Manager Library

## Fuentes y orden de revisión

Leer primero `spec-.net/spec.md` y `spec-python/spec.md` de `../test-manager-library-3145555-docs/`: alcance, HU, CA, reglas y RNF. Después revisar los `plan.md` y las `constitution.md` para organizar el código y aplicar SOLID. Completar con architecture, data-model, api-contract, tasks y ADR de la misma variante.

Los planes describen .NET 8/C# 12, ASP.NET Core, EF Core 8, BCrypt factor 12, xUnit; o Python 3.12, FastAPI, SQLAlchemy 2/Alembic, Argon2id, pytest. Ambas variantes usan PostgreSQL 16 y JWT HS256 de 8 horas. La traducción anterior a Laravel no está respaldada por estos planes. El esqueleto PHP existente requiere alineación; no se elige ni mezcla aquí una variante.

## Ramas hijas

Formato en minúsculas: `hu-<número de dos dígitos>-<rama base>`. Ejemplo: `hu-01-dev`, hija de dev; desde qa: `hu-01-qa`. El número identifica una HU del spec, no una tarea técnica.

Las ramas locales HU-01-health-check de api, app, infra, page y tool- se renombraron a `hu-01-dev`. Esto no acredita implementación de HU-01. La rama documental feature/branch-organization no representa una HU.

```bash
git switch dev
git switch -c hu-02-dev
```

## Historias reales

| HU | Rama desde dev | Alcance del spec |
|---|---|---|
| HU-01 | hu-01-dev | Iniciar sesión, token 8 horas, 401 genérico, protección y autorización |
| HU-02 | hu-02-dev | Alta de bibliotecarios por admin, usuario normalizado/único, rechazo de admin por API |
| HU-03 | hu-03-dev | Libros, ISBN único activo, ejemplares, portada JPG/PNG hasta 2 MB, baja lógica |
| HU-04 | hu-04-dev | Buscar libros activos, filtros, orden, paginación hasta 50 y total |
| HU-05 | hu-05-dev | Crear/consultar socios, documento único, sin eliminación |
| HU-06 | hu-06-dev | Préstamos de 1 a 3 líneas, máximo 3 sin devolver, 14 días, atomicidad, valores congelados |
| HU-07 | hu-07-dev | Devolución por línea, sin doble incremento, cierre calculado |
| HU-08 | hu-08-dev | Consultar/listar préstamos, filtros, estado calculado |
| HU-09 | hu-09-dev | Vencidos ordenados por retraso, acceso admin/librarian |
| HU-10 | hu-10-dev | Reporte por libro/categoría congelada, rango válido, solo admin |

Todos los CA del spec son obligatorios; la tabla es un resumen. Health check es T-01, infraestructura T-20, sembrador T-21, frontend T-22 y página pública T-23. Ninguna de esas tareas se convierte en una HU nueva.

## Requisitos no funcionales

| RNF | Evidencia requerida |
|---|---|
| RNF-1 | Búsqueda menor de 300 ms con 5 000 libros; carga con tool |
| RNF-2 | Dos préstamos del último ejemplar: uno gana, otro recibe 409 |
| RNF-3 | Contraseñas sin transmisión/almacenamiento en claro ni logs |
| RNF-4 | Cuerpo de error único según api-contract |
| RNF-5 | Arranque con un comando, motor inicialmente vacío y README de infra |

## Organización y SOLID según constitution

- I: dominio puro, solo biblioteca base/estándar; sin framework ni ORM.
- II: aplicación conoce dominio y define puertos; adaptadores los implementan; firmas sin tipos de framework.
- III: composición única en `src/Library.Bootstrap/Composition/PortBindings.cs` o `src/library/bootstrap/composition/port_bindings.py`.
- IV/SRP: un servicio por caso de uso. OCP: cambiar disco por S3 mediante adaptador. LSP: fakes sustituibles con iguales expectativas. ISP: puertos pequeños. DIP: puertos definidos por quien los consume.
- V: esquema, restricciones y semilla pertenecen a migraciones; infra solo motor vacío.
- VI–VIII: imponer invariantes posibles en la base, marcar pendientes, calcular estados/retrasos, preservar valores congelados.
- IX–XI: secretos desde entorno, .env ignorado; código/columnas/rutas en inglés y documentación/mensajes en español.
- XII: tarea terminada solo con evidencia ejecutable. Arquitectura verificada con NetArchTest en .NET o import-linter y tests de arquitectura en Python.

No añadir multas, pagos, reservas, renovaciones, correo/SMS, importación masiva ni atributos de libro fuera del spec.

## Estado

Infra contiene PostgreSQL vacío. API tiene un esqueleto Laravel fuera de los planes; app, page y tool tienen documentación inicial. HU-01 y T-20 siguen pendientes. Antes de implementar cada cambio, contrastar CA, RNF, artículos y evidencias; seguir el orden del plan y dependencias de tasks.
