# Organización de ramas

Ramas hijas en minúsculas: hu-NN-dev (ejemplo hu-01-dev). El número corresponde a la HU real del spec. HU-01 es iniciar sesión; health check es T-01. Integrar avances mediante commits pequeños Conventional Commits en inglés.

Se usa React y Laravel como exige el README original; no Python ni .NET. Se traducen las herramientas, preservando puertos/adaptadores, SOLID, datos, contrato y ADR.

Cada HU debe documentar sus CA, implementación, pruebas ejecutadas y pendientes. Las otras HU se implementan en sus ramas hu-02-dev hasta hu-10-dev y se integran conservando la historia.
