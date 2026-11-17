# tdt-tv-lista

Lista de canales y recetas que consume la app **TDT TV** (Android TV).

- `canales.m3u`: canales en orden de zapping. La URL de cada entrada es la página oficial del directo.
- `recipes.json`: ajustes por sitio web (CSS para ocultar avisos, JS para dar play, selector del botón de subtítulos).

La app descarga ambos ficheros de `https://raw.githubusercontent.com/<usuario>/tdt-tv-lista/main/` al arrancar.
Para cambiar la lista basta con hacer `git push`; no hay que recompilar el APK (GitHub tarda unos 5 minutos en refrescar la caché).

Formato completo: ver el README de la app `tdt-tv`.
