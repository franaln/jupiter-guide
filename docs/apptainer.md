# Containers con Apptainer

Las imágenes `.sif` están disponibles en el nodo principal en `/opt/images` y también en `/mnt/R5/images`.

## Crear una imagen a partir de una de Docker

```bash
apptainer build <image-name>.sif docker://<path-to-image>
```

O a partir de un archivo exportado con Docker:

```bash
docker save <path-to-image> -o <image-name>.tar
apptainer build <image-name>.sif docker-archive://<image-name>.tar
```

## Correr una imagen

```bash
apptainer run /opt/images/mg-pythia-delphes-latest.sif
```

Estas imágenes también se pueden usar en HTCondor: ver [Condor + Apptainer](htcondor.md#condor-apptainer).

- Documentación: <https://apptainer.org/docs/user/latest/>
