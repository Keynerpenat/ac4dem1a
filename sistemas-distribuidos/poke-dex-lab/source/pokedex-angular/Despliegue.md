# Presentado por: Keyner Peña

## Paso a Paso: Desplegar una Aplicación desde GitHub

Este documento describe cómo desplegar una aplicación desde un repositorio de GitHub utilizando Azure.

## Requisitos Previos

- **Cuenta en GitHub**: Asegúrate de tener una cuenta registrada en GitHub.

## Paso 1: Clonar el Repositorio

1. **Buscar el Repositorio**: Accede al repositorio que deseas clonar. En este caso, el enlace es: [Repositorio Poke-Dex-Lab](https://github.com/rcuello/ac4dem1a/tree/master/sistemas-distribuidos/poke-dex-lab).

2. **Crear un Fork**: Retrocede hasta la carpeta `master`, donde se habilitará la opción **FORK** (Bifurcación). Selecciona tu cuenta personal como destino y espera unos momentos hasta que se complete el proceso.

## Paso 2: Ingresar a Azure Portal

1. **Acceder a Azure**: Inicia sesión en el [Azure Portal](https://portal.azure.com).

2. **Crear una Aplicación Web Estática**: Dirígete a la opción de **Static Web App** y selecciona **Crear**.

## Paso 3: Configurar el Despliegue

1. **Nombre de la Aplicación**: En el campo de nombre de la aplicación web estática, ingresa: `swa-listrace-portal-prod-[S U-INICIAL]`. Por ejemplo: `swa-listrace-portal-prod-MVC`.

2. **Hospedaje**: Selecciona la opción **Gratis**.

3. **Origen de la Implementación**: Escoge **GitHub** y selecciona tu cuenta donde tienes el repositorio de la aplicación.

4. **Tecnologías**: Selecciona **Angular**.

5. **Dirección de la Aplicación**: Ingresa `./sistemas-distribuidos/poke-dex-lab/source/pokedex-angular`.

6. **Ubicación de la API**: No ingreses nada en este campo.

7. **Ubicación de Salida**: Coloca `dist/pokedex-angular`.

8. **Revisar y Crear**: Selecciona **Revisar y Crear**, y luego haz clic en **Crear**.

## Paso 4: Acceder a la Aplicación Desplegada

1. **Obtener el Enlace**: Una vez que el despliegue esté completo, selecciona el enlace de la página y pégalo en tu navegador. El enlace de la aplicación es: [Aplicación Desplegada]((https://wonderful-pond-060f67410.6.azurestaticapps.net/)).

## Paso 5: Mejorar la Seguridad

1. **Crear Archivo de Configuración**: Regresa al repositorio en GitHub donde se encuentra el archivo `angular.json`. En la misma carpeta, crea un nuevo archivo JSON llamado `staticwebapp.config.json` con el siguiente contenido:

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
 2. **Guardar y Hacer Commit: Guarda el archivo y realiza un commit. Azure implementará automáticamente los cambios en el despliegue.
    
## Paso 6: Verificar la seguridad

Para verificar el nivel de seguridad de nuestra página desplegada, seguiremos estos pasos:

1. Acceder al sitio web de análisis de seguridad: [securityheaders.com](https://securityheaders.com)
2. En el campo de texto principal de la página, copiaremos y pegaremos la URL de nuestra página desplegada
3. Presionaremos enter o haremos clic en el botón de análisis
