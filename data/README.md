# Datos

Los GeoTIFF y los parches **no se suben a GitHub** por su tamaño. Esta carpeta guarda solo la estructura.

```
data/
├── raw/         6 GeoTIFF exportados desde Google Earth Engine (cuadrícula 3×2)
└── processed/   parches.npz, lo genera el notebook (sección 3)
```

## Cómo obtenerlos

1. En `pipeline_vae_pino.ipynb`, cambia `GEE_PROJECT` por tu proyecto de Google Earth Engine y pon `RUN_GEE = True`.
2. Corre la sección 1: lanza la exportación a Google Drive (carpeta `tesis_vae`).
3. Descarga los 6 archivos `piloto_biobio_2023_v2_worldcover-*.tif` y déjalos en `data/raw/`.
4. Corre el resto del notebook: la sección 3 crea `data/processed/parches.npz`.

## Qué tiene cada GeoTIFF

- EPSG:32718 (UTM 18S), 10 m por píxel, zona lon −73,20 a −72,40 y lat −37,60 a −36,80 (Biobío).
- 13 bandas, `int16`: `preV_NDVI`, `preV_NBR`, `preV_BSI`, `preO_NDVI`, `preO_NBR`, `preO_BSI`,
  `post_NDVI`, `post_NBR`, `post_BSI`, `slope`, `pine`, `burned_dnbr`, `burned_ref`.
- Índices ×10000, pendiente ×100, NODATA = −32768.

| Compuesto | Fechas | Escenas |
|---|---|---|
| preV (antes del incendio, verano) | 2022-12-01 a 2023-01-25 | 51 |
| preO (otoño anterior) | 2022-03-01 a 2022-04-30 | 49 |
| post (después del incendio) | 2023-03-01 a 2023-04-30 | 41 |

Fuentes: Sentinel-2 L2A (máscara de nubes SCL, mediana), Copernicus DEM GLO-30 (pendiente),
ESA WorldCover 2021 (máscara de árboles) y MODIS MCD64A1 (área quemada de referencia).
