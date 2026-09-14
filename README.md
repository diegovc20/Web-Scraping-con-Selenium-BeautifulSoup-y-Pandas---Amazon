# Web Scraping con Selenium, BeautifulSoup y Pandas - Amazon

Script en Python que busca un producto en Amazon México, recorre varias páginas
de resultados y guarda los datos de cada producto en un archivo CSV.

**Autor:** Diego Valle Cuevas  
**Grupo:** 952  
**Actividad:** Meta 1.4 - Web Scraping

## ¿Qué hace?

El script abre un navegador Chrome controlado por Selenium y busca el producto
que el usuario indique en Amazon México. Por cada página de resultados que
visita (el número de páginas también lo decide el usuario), toma el HTML de la
página y con BeautifulSoup extrae los datos de cada producto.

Al final, con pandas, junta todo en un DataFrame y lo guarda en un archivo CSV.

## Datos que recolecta

De cada producto se guardan 5 columnas:

- **pagina** - en qué página de resultados salió
- **nombre** - el título del producto
- **precio** - el precio, ejemplo: $209.00
- **rating** - la calificación, ejemplo: 4.6 de 5 estrellas
- **entrega** - la fecha de entrega

Si un producto no trae alguno de estos datos (por ejemplo productos nuevos que
todavía no tienen calificación), se rellena con un valor por default
("Sin precio", "Sin calificacion", "Sin fecha de entrega") para que no queden
celdas vacías en el CSV.

## Requisitos

- Python 3.10 o superior
- Google Chrome instalado
- Selenium 4.1 o superior
- BeautifulSoup4
- Pandas

## Instalación

1. Clona este repositorio:

```
git clone https://github.com/diegovc20/Web-Scraping-con-Selenium-BeautifulSoup-y-Pandas---Amazon.git
cd Web-Scraping-con-Selenium-BeautifulSoup-y-Pandas---Amazon
```

2. (Opcional pero recomendado) Crea un entorno virtual:

```
python3 -m venv .venv
source .venv/bin/activate
```

3. Instala las librerías:

```
pip install selenium beautifulsoup4 pandas
```

No es necesario descargar el ChromeDriver por separado, desde Selenium 4.6+
se gestiona automáticamente.

## Cómo correrlo

Desde la terminal, dentro de la carpeta del proyecto:

```
python WebScrapping_df.py
```

El script te va a preguntar dos cosas directamente en la terminal:

```
¿Qué producto quieres buscar?
¿Cuántas páginas quieres visitar?
```

Mientras corre, va imprimiendo cuántos productos encontró en cada página.
Al terminar imprime el DataFrame completo y genera el archivo CSV en la misma
carpeta, con el nombre `amazon_producto_buscado.csv`.

## Ejemplo

Si buscas "audifonos" en 2 páginas, se genera el archivo `amazon_audifonos.csv`
con alrededor de 96 productos (Amazon muestra cerca de 48 por página).

## Notas

- El script usa un user-agent de Chrome para que Amazon no lo bloquee.
- Hay una pausa de 5 segundos por página para darle tiempo de cargar y para no
  saturar el servidor.
- Si en alguna página no encuentra productos, se detiene y guarda lo que
  alcanzó a recolectar.
