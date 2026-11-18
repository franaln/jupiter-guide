# Guía de usuarios de JUPITER

Fuente en Markdown de la guía publicada en https://franaln.github.io/jupiter-guide/

- Las páginas están en `docs/`; el menú se define en `mkdocs.yml` (`nav`).
- Cada push a `main` publica la guía automáticamente (GitHub Actions).
- **No incluir** IPs, datos de la VPN, usuarios ni contraseñas: es un repositorio público.

Vista previa local:

```bash
python3 -m venv .venv && .venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve
```
