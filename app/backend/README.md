# Backend de la Aplicación: Azure Search OpenAI Demo

Este directorio contiene el código fuente del backend de la aplicación **Azure Search OpenAI Demo**. El backend está desarrollado en Python utilizando el framework [Quart](https://quart.palletsprojects.com/) y es responsable de manejar la lógica del servidor, la gestión de datos y la integración con servicios de Azure como Cognitive Search y OpenAI.

## Tabla de Contenidos

- [Descripción](#descripción)
- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Uso](#uso)
- [Pruebas](#pruebas)
- [Contribución](#contribución)
- [Licencia](#licencia)

## Descripción

El backend proporciona una API RESTful para interactuar con el frontend y otros servicios. Incluye funcionalidades como:

- Integración con Azure Cognitive Search para búsqueda de documentos.
- Uso de Azure OpenAI para generación de texto y embeddings.
- Control de acceso basado en usuarios y grupos de Microsoft Entra.
- Soporte para carga y procesamiento de documentos.

## Requisitos

Antes de comenzar, asegúrate de tener instalados los siguientes requisitos:

### Requisitos de Software
- Python 3.8 o superior.
- [Poetry](https://python-poetry.org/) para la gestión de dependencias.
- Una cuenta de Azure con los siguientes servicios configurados:
  - Azure Cognitive Search.
  - Azure OpenAI.
  - Azure Storage.

### Dependencias Principales
El backend utiliza las siguientes dependencias clave, que se instalan automáticamente al ejecutar `poetry install`:

- `azure-ai-documentintelligence==1.0.0b4`: Para el análisis de documentos.
- `azure-cognitiveservices-speech==1.40.0`: Para servicios de voz.
- `azure-search-documents==11.6.0b9`: Para la integración con Azure Cognitive Search.
- `azure-storage-blob==12.22.0`: Para la gestión de blobs en Azure Storage.
- `quart==0.20.0`: Framework web utilizado para el backend.
- `opentelemetry-instrumentation-fastapi==0.47b0`: Para la instrumentación de FastAPI.
- `pydantic==2.8.2`: Para la validación de datos.
- `python-dotenv==1.0.1`: Para la gestión de variables de entorno.

Consulta el archivo [`requirements.txt`](app/backend/requirements.txt) para ver la lista completa de dependencias.

### Requisitos del Sistema
- Sistema operativo: Windows, macOS o Linux.
- Espacio en disco: Al menos 1 GB para dependencias y archivos temporales.
- Memoria RAM: Al menos 4 GB.

## Instalación

1. Clona este repositorio:

   ```bash
   git clone https://github.com/tu-repositorio.git
   cd app/backend
   ```

2. Instala las dependencias utilizando Poetry:

   ```bash
   poetry install
   ```

3. Configura las variables de entorno necesarias (ver sección [Configuración](#configuración)).

## Configuración

El backend utiliza variables de entorno para la configuración. Crea un archivo `.env` en el directorio `app/backend` con el siguiente contenido:

```env
AZURE_SEARCH_SERVICE=<nombre-del-servicio>
AZURE_SEARCH_INDEX=<nombre-del-índice>
AZURE_OPENAI_SERVICE=<nombre-del-servicio-openai>
AZURE_OPENAI_CHATGPT_MODEL=<modelo-chatgpt>
AZURE_STORAGE_ACCOUNT=<nombre-de-la-cuenta-de-almacenamiento>
AZURE_STORAGE_CONTAINER=<nombre-del-contenedor>
AZURE_TENANT_ID=<id-del-tenant>
AZURE_CLIENT_APP_ID=<id-de-la-aplicación-cliente>
AZURE_SERVER_APP_ID=<id-de-la-aplicación-servidor>
AZURE_SERVER_APP_SECRET=<secreto-de-la-aplicación-servidor>
```

Asegúrate de reemplazar los valores con los de tu entorno.

## Uso

Para iniciar el servidor de desarrollo, ejecuta el siguiente comando:

```bash
poetry run python -m quart --app app:app run --port 50505 --host localhost --reload
```

El servidor estará disponible en `http://localhost:50505`.

### Ejemplo de Uso

#### Obtener información de búsqueda

Realiza una solicitud GET al endpoint `/api/search`:

```bash
curl -X GET http://localhost:50505/api/search?q=example
```

#### Cargar un documento

Realiza una solicitud POST al endpoint `/api/upload`:

```bash
curl -X POST http://localhost:50505/api/upload \
     -H "Content-Type: multipart/form-data" \
     -F "file=@document.pdf"
```

## Pruebas

Para ejecutar las pruebas, utiliza el siguiente comando:

```bash
poetry run pytest
```

Asegúrate de que todas las pruebas pasen antes de realizar cambios en el código.

## Contribución

Si deseas contribuir al desarrollo del backend:

1. Crea un fork del repositorio.
2. Crea una rama para tu funcionalidad o corrección de errores (`git checkout -b feature/nueva-funcionalidad`).
3. Realiza tus cambios y realiza commits descriptivos.
4. Envía un pull request a la rama principal.

Por favor, revisa el archivo [CONTRIBUTING.md](../../CONTRIBUTING.md) para más detalles.

## Licencia

Este proyecto está licenciado bajo los términos de la [Licencia MIT](../../LICENSE).