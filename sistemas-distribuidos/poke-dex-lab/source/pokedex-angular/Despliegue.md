# Paso a Paso: Desplegar una Aplicacion desde GitHub

Este documento describe como desplegar una aplicaci贸n desde un repositorio de GitHub utilizando Azure.

## Requisitos Previos

- **Cuenta en GitHub**: Asegurate de tener una cuenta registrada en GitHub.

## Paso 1: Clonar el Repositorio

1. **Buscar el Repositorio**: Accede al repositorio que deseas clonar. En este caso, el enlace es: [Repositorio Poke-Dex-Lab](https://github.com/rcuello/ac4dem1a/tree/master/sistemas-distribuidos/poke-dex-lab).

2. **Crear un Fork**: Retrocede hasta la carpeta `master`, donde se habilitar谩 la opci贸n **FORK** (Bifurcaci贸n). Selecciona tu cuenta personal como destino y espera unos momentos hasta que se complete el proceso.

## Paso 2: Ingresar a Azure Portal

1. **Acceder a Azure**: Inicia sesi贸n en el [Azure Portal](https://portal.azure.com).

2. **Crear una Aplicaci贸n Web Est谩tica**: Dir铆gete a la opci贸n de **Static Web App** y selecciona **Crear**.

## Paso 3: Configurar el Despliegue

1. **Nombre de la Aplicaci贸n**: En el campo de nombre de la aplicaci贸n web est谩tica, ingresa: `swa-listrace-portal-prod-[S U-INICIAL]`. Por ejemplo: `swa-listrace-portal-prod-MVC`.

2. **Hospedaje**: Selecciona la opci贸n **Gratis**.

3. **Origen de la Implementaci贸n**: Escoge **GitHub** y selecciona tu cuenta donde tienes el repositorio de la aplicaci贸n.

4. **Tecnolog铆as**: Selecciona **Angular**.

5. **Direcci贸n de la Aplicaci贸n**: Ingresa `./sistemas-distribuidos/poke-dex-lab/source/pokedex-angular`.

6. **Ubicaci贸n de la API**: No ingreses nada en este campo.

7. **Ubicaci贸n de Salida**: Coloca `dist/pokedex-angular`.

8. **Revisar y Crear**: Selecciona **Revisar y Crear**, y luego haz clic en **Crear**.

## Paso 4: Acceder a la Aplicaci贸n Desplegada

1. **Obtener el Enlace**: Una vez que el despliegue est茅 completo, selecciona el enlace de la p谩gina y p茅galo en tu navegador. El enlace de la aplicaci贸n es: [Aplicaci贸n Desplegada](https://delightful-tree-03be9381e.6.azurestaticapps.net/?version=9).

## Paso 5: Mejorar la Seguridad

1. **Crear Archivo de Configuraci贸n**: Regresa al repositorio en GitHub donde se encuentra el archivo `angular.json`. En la misma carpeta, crea un nuevo archivo JSON llamado `staticwebapp.config.json` con el siguiente contenido:

   ```json
  {
  "globalHeaders": {
    "Content-Security-Policy": "default-src 'self' https://pokeapi.co; connect-src *; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src * data:; font-src 'self';",
    "X-Frame-Options": "DENY",
    "Permissions-Policy": "geolocation=(), camera=(), microphone=()",
    "Strict-Transport-Security": "max-age=63072000; includeSubDomains; preload"
  },
  "navigationFallback": {
    "rewrite": "/index.html"
  }
}
 2. **Guardar y Hacer Commit: Guarda el archivo y realiza un commit. Azure implementar谩 autom谩ticamente los cambios en el despliegue.
    
## Paso 6: Verificar la seguridad

Para verificar el nivel de seguridad de nuestra p谩gina desplegada, seguiremos estos pasos:

1. Acceder al sitio web de an谩lisis de seguridad: [securityheaders.com](https://securityheaders.com)
2. En el campo de texto principal de la p谩gina, copiaremos y pegaremos la URL de nuestra p谩gina desplegada
3. Presionaremos enter o haremos clic en el bot贸n de an谩lisis

**Resultado esperado:**
El sitio nos mostrar谩 un reporte de seguridad donde podremos observar que nuestra p谩gina tiene un nivel de seguridad **A**, que es la calificaci贸n m谩s alta posible.

Este resultado indica que nuestra p谩gina implementa correctamente todas las cabeceras de seguridad recomendadas.
