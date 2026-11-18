# Python, GPU y Jupyter

## Virtual environments

Hay varios environments configurados para usar con la GPU en `/opt/venvs`. Tienen los paquetes usuales (numpy, pandas, matplotlib, …), xgboost y keras o pytorch con CUDA:

| Environment | Incluye |
| --- | --- |
| `ml` | Keras 3 |
| `ml-keras2` | Keras 2 |
| `ml-torch` | PyTorch |

También podés crear el tuyo en tu home o en el directorio compartido `/opt/venvs-hep`.

Crear un environment:

```bash
make_venv <name> [requirements.txt]
```

Hacerlo disponible para usar desde un notebook:

```bash
install_env_kernel /opt/venvs-hep/<name>
```

Ver los environments disponibles:

```bash
list_venvs
```

Activar uno:

```bash
load_venv <name>
```

o

```bash
source /path-to-venv/bin/activate
```

Y desactivarlo:

```bash
deactivate
```

## Conda environments

Conda se usa de forma similar:

```bash
conda env list
conda activate ml
```

Crear un environment propio (queda en `/home/<user>/.conda/envs`):

```bash
conda create -n <name>
```

Hay un directorio compartido, con permisos para todos, donde se pueden crear y modificar environments: `/opt/conda-envs-hep`.

Crear un environment compartido:

```bash
conda create -p /opt/conda-envs-hep/<env-name> python=3.11 numpy matplotlib
```

Actualizar uno existente:

```bash
conda activate /opt/conda-envs-hep/<env-name>
conda install scipy
```

Hacerlo disponible para usar desde un notebook:

```bash
install_env_kernel /opt/conda-envs-hep/<env-name>
```

## GPU

El nodo principal tiene una GPU RTX 3090 para machine learning.

!!! warning ""
    **Chequeá el uso de la GPU antes de usarla.** Podés ver su estado con `nvidia-smi` o `nvtop`.

**Keras:** por defecto usa la GPU. Para deshabilitarla:

```python
os.environ["CUDA_VISIBLE_DEVICES"] = "-1"
```

**PyTorch:**

```python
if use_gpu:
    device = torch.device("cuda")
else:
    device = torch.device("cpu")
```

**xgboost:**

```python
xgb_model = xgb.XGBRegressor(tree_method="hist", device="cuda")
```

## Jupyter notebooks

También podés usar la GPU desde un notebook en tu computadora, con VSCode o con Jupyter en el navegador.

### VSCode

1. Conectate a `jupiter` con Remote-SSH.
2. En un notebook, elegí **Select Kernel → Jupyter Kernel** y el kernel que quieras usar.
3. Si no lo detecta automáticamente, usá **Select interpreter** con el path del environment (por ejemplo `/opt/venvs/ml/bin/python`) y después **Select Kernel** con ese mismo environment.

### Jupyter en el navegador

En el cluster, activá el environment y arrancá el server:

```bash
load_venv ml
jupyter lab --no-browser --port 9999
```

Eso muestra una dirección con el puerto y un token, por ejemplo:

```
http://localhost:9999/lab?token=<token>
```

En tu computadora, redirigí ese puerto:

```bash
ssh -NfL localhost:9999:localhost:9999 <user>@jupiter
```

Y abrí esa misma dirección en el navegador.

!!! tip ""
    Si el puerto 9999 ya lo usa otra persona, elegí otro número.
