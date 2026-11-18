# ATLAS

## CVMFS y software de ATLAS

CVMFS está montado en el nodo principal y en todos los nodos de cómputo, así que se usa igual que en lxplus, también en los jobs de HTCondor:

```bash
setupATLAS
lsetup rucio
```

## Proxy de la grid

`voms-proxy-init` está instalado en `jupiter`, así que no hace falta `setupATLAS` para generar el proxy:

```bash
voms-proxy-init -voms atlas
```

## MCP para Claude Code (Rucio y AMI)

Hay dos servidores MCP instalados que le permiten a Claude Code consultar **Rucio** (datasets, réplicas, reglas) y **AMI** (metadata, secciones eficaces, tags). Los dos son de solo lectura.

1. Generá tu proxy:

    ```bash
    voms-proxy-init -voms atlas
    ```

2. Agregá los MCP a Claude Code (una sola vez):

    ```bash
    claude mcp add --scope user rucio-atlas -- rucio-mcp-atlas
    ```

    ```bash
    claude mcp add --scope user ami -- ami-mcp-atlas
    ```

!!! note
    Si tu cuenta de Rucio no es igual a tu usuario de `jupiter`, agregá `-e RUCIO_ACCOUNT=<tu_cuenta>` en el primer `claude mcp add`.

Cuando venza el proxy, repetí el paso 1.

## SALT

### Instalación general

Si no necesitás editar el código, podés usar el environment de conda `upp-salt` (Python 3.12, con `umami-preprocessing` y `salt-ml` de PyPI):

```bash
conda activate upp-salt
```

Preprocessing:

```bash
preprocess --config CONFIG.yml --split=all
```

Training:

```bash
salt fit --config CONFIG.yml
```

### Environment propio

La otra opción es crear tu propio environment (conda, venv o uv) e instalar SALT siguiendo la documentación:

- <https://umami-hep.github.io/umami-preprocessing/setup/>
- <https://ftag-salt.docs.cern.ch/setup>

Los archivos del tutorial están en `/mnt/R5/ATLAS/salt_tutorial/training-samples-public`.
