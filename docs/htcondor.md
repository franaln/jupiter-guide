# HTCondor

Hay 6 nodos de cómputo con un total de ~20 slots. Todos tienen:

- AlmaLinux 9
- Acceso a `/mnt/R5`
- Las imágenes de Apptainer de `/mnt/R5/images`, sincronizadas en `/opt/images`
- Acceso a CVMFS

## Comandos útiles

Mandar jobs al cluster:

```bash
condor_submit <submit_file.sub>
```

!!! tip "Notificaciones por mail"
    Para recibir un mail cuando los jobs terminan o tienen algún problema, agregá al archivo `.sub`:

    ```
    notify_user = <tu-mail>
    notification = always
    ```

Ver los jobs en cola o corriendo:

```bash
condor_q
condor_q -analyze <job-id>
condor_q -better-analyze <job-id>
```

Ver el estado de los nodos:

```bash
condor_status
```

Eliminar un job:

```bash
condor_rm <job-id>
```

Ver el output de un job que está corriendo:

```bash
condor_tail <job-id>
```

Conectarse al nodo donde corre un job:

```bash
condor_ssh_to_job <job-id>
```

Ver los jobs terminados, o uno en particular:

```bash
condor_history | head
condor_history <job-id>
```

- Más información: <https://htcondor.readthedocs.io/en/latest/users-manual/quick-start-guide.html>

## Condor + Apptainer

Para correr los jobs dentro de una imagen de Apptainer:

```
universe = container
container_image = <image-name>.sif
```

La imagen puede estar en cualquier path y se transfiere a cada nodo. Si es una de las que están en `/opt/images`, conviene usar el path completo: cada nodo usa su copia local y no hace falta transferirla en cada job, que es más rápido.

```
universe = container
container_image = /opt/images/<image-name>.sif
```

Para que una imagen esté disponible en `/opt/images`, copiala a `/mnt/R5/images` y se sincroniza sola en todos los nodos. Para forzar la sincronización en el momento:

```bash
sudo sync-images-now
```
