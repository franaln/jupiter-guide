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
