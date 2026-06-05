# Predictor de Grupos · Mundial 2026 ⚽

Simulador de la fase de grupos de la Copa del Mundo 2026. Elegís un grupo (o lo armás con
las 48 selecciones clasificadas) y corre **30.000 simulaciones Monte Carlo** para estimar la
probabilidad de cada equipo de clasificar.

- Sitio 100% estático: un solo `index.html`, sin backend, sin API, sin build.
- Motor de predicción: rating estilo **Elo** por selección + goles por **distribución de Poisson**.
- Bonus de localía para los anfitriones (México, EE. UU., Canadá).
- Grupos oficiales A–L precargados (incluye las repescas: Chequia, Bosnia, Turquía, Suecia, Irak, RD Congo).

## Subirlo a GitHub Pages

1. Creá un repositorio nuevo en GitHub (por ejemplo `predictor-mundial-2026`).
2. Subí el archivo `index.html` a la raíz del repo (botón **Add file → Upload files**, o por git):
   ```bash
   git init
   git add index.html
   git commit -m "Predictor de grupos Mundial 2026"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/predictor-mundial-2026.git
   git push -u origin main
   ```
3. En el repo, andá a **Settings → Pages**.
4. En **Build and deployment → Source** elegí **Deploy from a branch**.
5. Branch: `main`, carpeta `/ (root)`. Guardá.
6. En ~1 minuto tu sitio queda en:
   `https://TU_USUARIO.github.io/predictor-mundial-2026/`

Listo. Cualquier cambio que pushees a `main` se publica solo.

## Ajustar el modelo

Todo está en el `<script>` dentro de `index.html`:

- **Ratings**: objeto `T` (`"Selección": ["bandera", elo]`). Subí/bajá el número para cambiar la fuerza.
- **Goles esperados**: función `lambdas()` — el divisor `150` controla cuánto pesa cada punto de Elo
  (más chico = partidos más predecibles).
- **Localía**: constante `HOSTS` y el `+40` en `effElo()`.
- **Cantidad de simulaciones**: el `30000` dentro de `run()`.

## Nota

Clasifican los 2 primeros de cada grupo **más los 8 mejores terceros**. El puesto de cada equipo
y su % de pasar como top 2 se modelan acá; el repechaje de mejores terceros depende de los otros
grupos y no se calcula. Pronóstico con fines de entretenimiento.
