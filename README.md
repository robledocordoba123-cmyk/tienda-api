# API de la Tienda

API hecha con FastAPI para la Guía 2 de la ficha 3229209 (ADSO). Tiene el CRUD de productos y de categorías, cada recurso en su propio archivo con APIRouter. Los datos de entrada se validan con Pydantic y por ahora se guardan en listas en memoria, así que vuelven a su estado inicial cada vez que se reinicia el servidor.

Integrantes: Manuela Córdoba Robledo y Davier Andrés Quinto Bejarano.

## Estructura

```
tienda-api/
|-- main.py               crea la app e incluye los routers
|-- requirements.txt
|-- capturas/             pruebas hechas en /docs
|-- routers/
|   |-- __init__.py
|   |-- productos.py      modelo y CRUD de productos
|   |-- categorias.py     modelo y CRUD de categorías
```

## Instalación

Se necesita Python 3 y pip.

```
git clone https://github.com/robledocordoba123-cmyk/tienda-api.git
cd tienda-api
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

En Linux o macOS el entorno se activa con `source venv/bin/activate`.

## Ejecución

```
uvicorn main:app --reload
```

Después se abre http://127.0.0.1:8000/docs para ver y probar los endpoints. Si el puerto 8000 está ocupado, se agrega `--port 8001` al comando y se entra por ese puerto.

## Endpoints

| Método | Ruta | Qué hace | Código de éxito |
|---|---|---|---|
| GET | `/productos` | Lista los productos | 200 |
| GET | `/productos/{producto_id}` | Devuelve un producto | 200 |
| POST | `/productos` | Crea un producto | 201 |
| PUT | `/productos/{producto_id}` | Actualiza un producto | 200 |
| DELETE | `/productos/{producto_id}` | Elimina un producto | 200 |
| GET | `/categorias` | Lista las categorías | 200 |
| GET | `/categorias/{categoria_id}` | Devuelve una categoría | 200 |
| POST | `/categorias` | Crea una categoría | 201 |
| PUT | `/categorias/{categoria_id}` | Actualiza el nombre de una categoría | 200 |
| DELETE | `/categorias/{categoria_id}` | Elimina una categoría | 200 |

Si el id no existe, la API responde 404. Si faltan datos o llegan con un tipo incorrecto, responde 422.

## Ejemplo

Para crear una categoría con `POST /categorias` se envía este cuerpo:

```json
{
  "nombre": "Almacenamiento"
}
```

Y la API responde 201:

```json
{
  "mensaje": "Categoria creada",
  "categoria": { "id": 4, "nombre": "Almacenamiento" }
}
```
