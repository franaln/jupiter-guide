# Simulaciones

## Imágenes de MadGraph + Pythia + Delphes

Imágenes de Docker y Apptainer disponibles:

| MadGraph | Pythia | Delphes | Docker | Apptainer | Dockerfile |
| --- | --- | --- | --- | --- | --- |
| 3.3.2 | 8.306 | 3.5.0 | `mg-pythia-delphes:3.3.2` | `mg-pythia-delphes-3.3.2.sif` | [Dockerfile](https://github.com/franaln/mg-pythia-delphes/blob/main/images/mg-pythia-delphes-3.3.2.Dockerfile) |
| 3.5.6 | 8.306 | 3.5.0 | `mg-pythia-delphes:3.5.6` | `mg-pythia-delphes-3.5.6.sif` | [Dockerfile](https://github.com/franaln/mg-pythia-delphes/blob/main/images/mg-pythia-delphes-3.5.6.Dockerfile) |

Modelos extra incluidos:

- `invisibleBA_UFO`
- `loop_qcd_qed_sm`
- `SM_LQHH_MU2-LAM3-LAM1-LAM2`
- `SM_LQs`

Más detalles en [GitHub](https://github.com/franaln/mg-pythia-delphes/tree/main/examples) y en [Docker Hub](https://hub.docker.com/r/franaln/mg-pythia-delphes).

En `jupiter`, ver las imágenes disponibles:

```bash
mgpd images
```

## Cómo usarlas

### Con Docker (fuera de jupiter)

Cargar la imagen con la versión que quieras:

```bash
docker run -it --rm franaln/mg-pythia-delphes:3.3.2
```

Adentro, configurar el entorno y usar MadGraph:

```bash
source /setup_mg_pythia_delphes.sh
mg5_aMC
```

### Con Apptainer en jupiter

```bash
apptainer run /opt/images/mg-pythia-delphes-3.3.2.sif
```

### Con HTCondor

En el archivo `.sub`:

```
universe = container
container_image = /opt/images/mg-pythia-delphes-latest.sif
...
```

Ver [Condor + Apptainer](htcondor.md#condor-apptainer).

### Script `run_mg_pythia_delphes.py`

Se corre con:

```bash
run_mg_pythia_delphes.py -c config.yml -o OUTPUT_DIR
```

donde `OUTPUT_DIR` es el directorio donde se guarda el output, relativo o con el path completo. Por ejemplo, en el RAID:

```bash
run_mg_pythia_delphes.py -c config.yml -o /mnt/R5/<user>/output_madgraph
```

Para unir los outputs de distintos jobs:

```bash
merge_mg_pythia_delphes_output.py -o output_directory input_files*.tar.gz
```

Todas las opciones: `merge_mg_pythia_delphes_output.py --help`.

- Más información: [README](https://github.com/franaln/mg-pythia-delphes/blob/main/README.md)
- Ejemplos de configuración: [examples](https://github.com/franaln/mg-pythia-delphes/tree/main/examples)

## mgpd: correr el workflow local o en HTCondor

Ejemplo con el directorio de configuración `project_pp_X` (con un `config.yml`) y el directorio de producción `/mnt/R5/<user>/project_pp_X_run_01`.

Crear un proyecto nuevo:

```bash
mgpd create project_pp_X --process "generate p p > ta+ ta-" --level detector --mode condor
```

Correr la producción en HTCondor:

```bash
mgpd run project_pp_X -o /mnt/R5/<user>/project_pp_X_run_01 --mode condor
```

Ver el estado de la producción:

```bash
mgpd status /mnt/R5/<user>/project_pp_X_run_01
```

Validar el output cuando termina:

```bash
mgpd validate-results /mnt/R5/<user>/project_pp_X_run_01
```

Recuperar jobs fallidos:

```bash
mgpd recover --plan /mnt/R5/<user>/project_pp_X_run_01 --json
mgpd recover /mnt/R5/<user>/project_pp_X_run_01 -o /mnt/R5/<user>/project_pp_X_retry_01
mgpd execute /mnt/R5/<user>/project_pp_X_retry_01
```

Unir el output:

```bash
mgpd merge /mnt/R5/<user>/project_pp_X_run_01
```

- Más información: [README](https://github.com/franaln/mg-pythia-delphes/blob/main/README.md)
- Ejemplos de configuración: [examples](https://github.com/franaln/mg-pythia-delphes/tree/main/examples)
