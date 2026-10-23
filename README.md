# Mapa de cobertura SUS

Mapa interactivo (Leaflet) con consultorios SUS, consulta externa, Pilares en operación y población/viviendas por manzana (CDMX).

## Cómo usarlo
- Abre `index.html` con doble clic (necesita internet para Leaflet y el mapa base) o publícalo con GitHub Pages / un servidor estático.
- Clic en un punto: círculo de 1.0 o 1.5 km con población, viviendas, unidades de consulta externa, SUS y Pilares dentro, y tiempo caminando estimado a la consulta externa más cercana.
- Botones del mapa (arriba a la izquierda): dibujar polígono o rectángulo, editar, mover y borrar.

## Datos (`datos/`)
| Archivo | Contenido |
|---|---|
| `sus.js` | 406 consultorios SUS |
| `consulta_externa.js` | 2,884 unidades (2,268 de consulta externa y 616 de hospitalización; el selector permite considerar solo las primeras) |
| `pilares.js` | 300 Pilares con su estatus (198 en operación); el estatus se ve al dar clic. Los conteos de círculos y polígonos solo cuentan los «En operación» |
| `mz/0.js … mz/15.js` | Manzanas simplificadas (3 m) en WGS84, un archivo por alcaldía; se cargan solo las que se muestran |
| `alcaldias.js` | Catálogo de alcaldías |
| `zonas_semaforo.js` | 2,551 zonas de trabajo con su Color Zona (semáforo verde, amarilla, naranja, roja) |
| `manzanas_centros.js` | Punto representativo de cada manzana con POBTOT y VIVTOT, para los cálculos |

Las capas originales venían en EPSG:32614 y se reproyectaron a WGS84 (EPSG:4326).

## Símbolos y colores
Íconos en `iconos/` (`sus.svg`, `cruz.svg`, `pilares.png`). Panel y símbolos con la paleta institucional (guinda #611232, dorado #a57f2c, verde #1e5b4f); el mapa de calor va de crema a rojo (#fef0d9 → #b30000).

## Método
- Población y viviendas de una zona = suma de las manzanas cuyo punto representativo cae dentro del círculo o polígono.
- Tiempo caminando = distancia en línea recta × 1.3 ÷ 4.8 km/h (constantes `VEL` y `FAC` en `index.html`). Es una estimación, no sigue calles.
- Clases del mapa de calor = quintiles de las manzanas con dato mayor a 0.

## Privacidad
Repositorio privado: los datos de ubicación de SUS y consulta externa no deben publicarse.
