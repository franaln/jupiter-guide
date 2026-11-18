# Almacenamiento

!!! warning ""
    Los datos almacenados **no tienen backup**.

## Home

Todos tienen un directorio en el home del nodo principal:

```
/home/<user>
```

Hay una copia de tu home del día anterior en `/mnt/R5/backup/home/<user>`.

!!! danger ""
    **No guardes datos grandes en el home:** para datos de gran tamaño usá `/mnt/R5`.

## Scratch (NVMe, 1 TB)

En el nodo principal hay espacio rápido para uso **temporal**, por ejemplo para entrenar con la GPU:

```
/scratch/<user>
```

## RAID (RAID5 HDD, 18 TB)

Para guardar datos con más espacio:

```
/mnt/R5/<user>
```

- No está en el nodo principal y es HDD, así que es más lento. Pero todos los nodos tienen acceso, así que se puede usar desde HTCondor.
- Para descargar datos directamente, podés entrar al nodo `n1` desde el nodo principal con el mismo usuario y password:

    ```bash
    ssh n1
    ```

## Directorios compartidos

En `/scratch` y `/mnt/R5`, además de los directorios de cada usuario, hay directorios compartidos:

| Directorio | Acceso |
| --- | --- |
| `HEP` | Todos |
| `ATLAS` | Solo usuarios de ATLAS |
| `Pheno` | Solo usuarios de Pheno |
