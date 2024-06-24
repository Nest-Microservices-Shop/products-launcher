## Dev

1. Clonar el repositorio
2. Crear un `.env` basado en el `.env.template`
3. Actualizar submodulos

```bash
git submodule update --init --recursive
```

4. Ejecutar el comando

```bash
docker compose up --build
```

### Pasos para crear los Git Submodules

1. Crear un nuevo repositorio en GitHub
2. Clonar el repositorio en la máquina local
3. Añadir el submodule, donde `repository_url` es la url del repositorio y `directory_name` es el nombre de la carpeta donde quieres que se guarde el sub-módulo (no debe de existir en el proyecto)

```bash
git submodule add <repository_url> <directory_name>
```

4. Añadir los cambios al repositorio (git add, git commit, git push)
   Ej:

```bash
git add .
git commit -m "Add submodule"
git push
```

5. Inicializar y actualizar Sub-módulos, cuando alguien clona el repositorio por primera vez, debe de ejecutar el siguiente comando para inicializar y actualizar los sub-módulos

```bash
git submodule update --init --recursive
```

6. Para actualizar las referencias de los sub-módulos

```bash
git submodule update --remote
```

## Pasos para sincronizar cambios desde los submodulos a los repositorios originales

1. Ubicarse dentro del directorio del submodulo, ejemplo:

```pwsh
cd /products-launcher/orders-ms
```

2. Agregar los cambios realizados en el modulo `git add .` o el que corresponda
3. Realizar un commit

```bash
git commit -m "commit message"
```

4. Realizamos el push a al repositorio original

```bash
git push origin main
```

4.1 En caso de que nos encontremos en la referencia de un commmit, ejemplo: `detached at f015f63`. Seguimos los pasos a continuacion.

- Luego de hacer el commit del paso 3: `git checkout -b temp-branch`
- Ejecutar `git add .`
- Realizar un commit `git commit -m "commit message"`
- Realizamos el push a `git push origin temp-branch`
- Cambiamos a la rama `main`: `git checkout main`
- Mergeamos la rama temporal `git merge temp-branch`
- Eliminamos la rama temporal `git branch -d temp-branch`
- Realizamos el push a `git push origin main`

5. Nos movemos a la raiz del reporitorio que contiene los submodulos `cd ../`
6. Agregamos el submodulo actualizado

```bash
git add [nombre-de-la-carpeta-del-submodulo]
```

7. Realizamos un commit para indicar que se ha actualizado el submodulo
8. Realizamos el push al main

## Importante

Si se trabaja en el repositorio que tiene los sub-módulos, **primero actualizar y hacer push** en el sub-módulo y **después** en el repositorio principal.

Si se hace al revés, se perderán las referencias de los sub-módulos en el repositorio principal y tendremos que resolver conflictos.

# Prod

## Opcion 1

NOTA: Esta opcion se basa el `docker-compose.prod.yml`, porque en este las imagenes se construyen en el proceso, por lo que no se ven en la necesidad de descargar ninguna imagen de `dockerhub`

1. Clonar el repositorio
2. Asegurarse de tener Docker Desktop instalado y corriendo
3. Crear un `.env` en base al `.env.template`
4. Ejecutar el comando

```bash
docker compose -f docker-compose.prod.yml up --build
```

## Opcion 2

NOTA: Esta opcion se basa el `docker-compose.dev.yml`, porque en este las imagenes se descargan desde mi cuenta de `dockerhub`, alli ya se encuentran construidas, ya sea la version `latest` o la `1.0.0`

1. Clonar el repositorio
2. Asegurarse de tener Docker Desktop instalado y corriendo
3. Crear un `.env` en base al `.env.template`
4. Ejecutar el comando

```bash
docker compose -f docker-compose.dev.yml up --build
```
