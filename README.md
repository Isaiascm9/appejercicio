# Pulso

App de entrenamiento en un solo archivo HTML. Sin backend, sin cuentas: tu progreso se guarda en el navegador.

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
- Exportación de todos tus datos a JSON.

## Publicar en GitHub Pages

1. Sube el contenido de esta carpeta a un repositorio.
2. En el repositorio: **Settings → Pages**.
3. En *Source* elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
4. Guarda. En un par de minutos la app queda en `https://<tu-usuario>.github.io/<repo>/`.

No hace falta ningún paso de compilación para publicar: el CSS ya viene compilado en `assets/`.

## Estructura

```
index.html              La app entera (HTML + CSS propio + JS)
assets/pulso.css        Tailwind compilado, solo las clases usadas (~10 KB)
assets/chart.umd.js     Chart.js, servido localmente
manifest.webmanifest    Permite instalarla como app en el móvil
src/input.css           Entrada de Tailwind (solo para recompilar)
tailwind.config.js      Configuración de Tailwind
```

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
