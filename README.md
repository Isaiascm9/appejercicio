# Pulso

App de entrenamiento sin backend ni cuentas. Funciona sin conexión y tu progreso se guarda en tu navegador.

## Qué hace

- **Plan personalizado** a partir de objetivo (grasa / músculo / fuerza), lugar de entrenamiento y nivel. El objetivo define las repeticiones y el tiempo de descanso.
- **33 ejercicios** con instrucciones de ejecución, separados en rutinas de casa (peso corporal) y de gimnasio (con carga).
- **10 rutinas completas**: empuje, tirón, pierna, cuerpo completo, cardio y más.
- **Registro serie por serie**: peso × repeticiones en gimnasio; repeticiones o segundos en casa.
- **Historial por ejercicio**: al entrenar ves lo que levantaste la última vez, y las series vienen precargadas con esos valores.
- **Récords personales** detectados automáticamente.
- **Cronómetro de descanso** que arranca solo al marcar una serie.
- **Progreso**: mapa de constancia de 12 semanas, historial de sesiones, gráfica de peso, totales de minutos y volumen.
- Registro de agua y macronutrientes.
- **Funciona sin internet**: se instala como app en el móvil y no hace ni una sola petición de red.
- Exportación de todos tus datos a JSON.

## Publicar en GitHub Pages

1. Sube el contenido de esta carpeta a un repositorio.
2. En el repositorio: **Settings → Pages**.
3. En *Source* elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
4. Guarda. En un par de minutos la app queda en `https://<tu-usuario>.github.io/<repo>/`.

No hace falta ningún paso de compilación: `index.html` ya lleva todo dentro.

El service worker **solo funciona sobre HTTPS o en `localhost`**. GitHub Pages
sirve HTTPS, así que ahí funciona. Si abres el archivo con doble clic
(`file://`), la app funciona pero sin modo offline gestionado.

## Estructura

```
index.html              La app entera: HTML, CSS, JS, fuentes y Chart.js incrustados
sw.js                   Service worker que la hace funcionar sin conexión
manifest.webmanifest    Datos para instalarla como app en el móvil
icons/                  Iconos de la app (192, 512, maskable, apple-touch)
assets/                 Piezas sueltas, solo para reconstruir index.html
src/input.css           Entrada de Tailwind
tailwind.config.js      Configuración de Tailwind
```

Los cuatro primeros son los que hay que subir. `assets/` y `src/` solo hacen falta si vas a modificar el diseño.

## Cómo funciona sin conexión

No hay ni una petición a servidores externos: Tailwind compilado, Chart.js y las
dos tipografías (Oswald y Work Sans, en formato variable) van incrustadas en el
propio `index.html`.

El service worker usa *network-first* para el HTML y *cache-first* para el resto.
En la práctica: si hay internet recibes la última versión publicada; si no la hay
—un gimnasio en sótano, el metro, un avión— la app abre igual desde la copia
guardada, con todo el historial intacto.

Para instalarla en el móvil: ábrela en el navegador y elige "Añadir a la pantalla
de inicio". Arranca a pantalla completa, sin barra de direcciones.

Puedes comprobar el estado en **Perfil → Sin conexión**.

> Al publicar una versión nueva, sube también `sw.js` con el número de `CACHE`
> cambiado (`pulso-v1` → `pulso-v2`). Si no, los navegadores que ya tengan la app
> guardada podrían seguir sirviendo la versión anterior.

## Recompilar el CSS

Solo hace falta si añades clases de Tailwind nuevas al HTML.

```bash
npm install
npx tailwindcss -i src/input.css -o assets/pulso.css --minify
```

## Dónde se guardan los datos

En `localStorage`, bajo la clave `pulso:v1`. Es decir: en tu navegador y tu dispositivo, no en un servidor. Consecuencias a tener en cuenta:

- Si borras los datos del navegador, se pierde el historial. Usa **Perfil → Exportar mis datos** para respaldarlo.
- No se sincroniza entre dispositivos. Para eso haría falta un backend.
- En navegación privada solo dura mientras la pestaña esté abierta.

La app detecta qué tipo de almacenamiento tiene disponible y lo indica en **Perfil → Almacenamiento**.

## Accesibilidad

Navegación completa por teclado con foco visible, etiquetas en todos los campos, anuncios con `aria-live` en las confirmaciones y respeto a `prefers-reduced-motion`.

## Aviso

Pulso es una herramienta de registro, no un sustituto de asesoría médica o de un entrenador. Consulta a un profesional antes de empezar un programa de entrenamiento, sobre todo si tienes alguna condición de salud o lesión previa.

## Licencia

MIT. Revisa el archivo `LICENSE` y pon tu nombre donde dice `<TU NOMBRE>`.
