# Documentación Técnica del Proyecto

## Descripción del Proyecto
Este proyecto implementa una aplicación web utilizando Svelte y Vite, enfocada en la visualización de datos mediante un efecto de scrollytelling. La aplicación ofrece un recorrido interactivo sobre los principios, la historia y los usos de la computación cuántica, presentando la información de manera dinámica conforme el usuario se desplaza por la página.

## Estructura del Proyecto
El proyecto está organizado de la siguiente manera:

- **public/**: Contiene los recursos públicos del proyecto, como imágenes, sonidos, etc.
- **src/**: Contiene el código fuente de la aplicación.
  - **components/**: Componentes de Svelte utilizados en la aplicación.
  - **App.svelte**: Componente principal de la aplicación.
- **index.html**: Archivo HTML principal.
- **jsconfig.json**: Configuración de JavaScript.
- **package.json**: Dependencias y scripts del proyecto.
- **svelte.config.js**: Configuración de Svelte.
- **vite.config.js**: Configuración de Vite.

## Requisitos de Instalación
1. **Node.js**: Asegúrese de tener Node.js instalado en su sistema.
2. **Dependencias del Proyecto**: Instale las dependencias ejecutando:
   ```bash
   npm install
   ```

## Uso del Proyecto
Para iniciar el proyecto en un entorno de desarrollo, ejecute:
```bash
npm run dev
```
Esto iniciará un servidor de desarrollo y podrá acceder a la aplicación.

## Características y Funcionalidades

### 1. Filtrado de Datos con `svelte-scroller`
El módulo `svelte-scroller` se utiliza para filtrar datos en función del desplazamiento del usuario. Esto permite una visualización de datos dinámica y reactiva que se adapta a la interacción del usuario. Para hacer uso del mismo se ha partido de la plantilla brindada en clase.


### 2. Animaciones con AOS (Animate On Scroll Library)
Se ha integrado AOS para añadir animaciones suaves y atractivas al desplazarse por la página. Esto mejora la experiencia del usuario al hacer que las visualizaciones y otros elementos de la página aparezcan de manera más dinámica y visualmente atractiva.


### 3. Funciones JavaScript

#### Cambio Automático de Imágenes - changeImage()
Esta función cambia automáticamente las imágenes en un intervalo de tiempo definido.

```javascript
let charts = {
  0: "entrelazamiento1.png",
  1: "entrelazamiento2.png",
  2: "entrelazamiento3.png",
  3: "entrelazamiento4.png",
};

let currentIndex = 0;
let currentImage = charts[currentIndex];

function changeImage() {
  setTimeout(() => {
    currentIndex = (currentIndex + 1) < 4 ? currentIndex + 1 : 0;
    currentImage = charts[currentIndex];
    changeImage(); // Llama a la función de nuevo para continuar el bucle
  }, 1000);
}

onMount(() => {
  changeImage();
});
```

#### Control de Reproducción de Audio - togglePlayback()
Esta función permite reproducir o pausar una canción al hacer clic en un botón.

```javascript
let cancion;
let reproduciendo = false;

onMount(() => {
  cancion = document.getElementById("cancion");
});

function togglePlayback() {
  if (!cancion) return;

  if (reproduciendo) {
    cancion.pause();
  } else {
    cancion.play();
  }

  reproduciendo = !reproduciendo;
}
```

#### Eventos Históricos de la Computación Cuántica 
Se define una lista de eventos históricos para ser mostrados en la aplicación. Para no tener grandes textos en cada “evento” del timeline, se toman los datos directamente desde este lugar.

```javascript
const events = [
  // Lista de eventos con sus propiedades
];
```

#### Variables para el Scroller
Estas variables se utilizan para controlar el comportamiento del scroller de los gráficos en diferentes secciones de la página. Son esenciales para el funcionamiento interactivo y dinámico de la aplicación.

```javascript
let count2, index2, offset2, progress2;
let top2 = 0.1, threshold2 = 0.5, bottom2 = 0.9;

let count3, index3, offset3, progress3;
let top3 = 0.1, threshold3 = 0.5, bottom3 = 0.9;

let count4, index4, offset4, progress4;
let top4 = 0.1, threshold4 = 0.5, bottom4 = 0.9;
```

### 4. Fondos Dinámicos de Estrellas
Para incorporar fondos dinámicos de estrellas en nuestra aplicación, comenzamos utilizando repositorios y ejemplos existentes como base. Adaptamos estos recursos para satisfacer los requisitos técnicos específicos de nuestro proyecto y los recursos visuales necesarios. A continuación, se presentan algunos de los recursos que utilizamos y modificamos:

- [Stars Animation Effect](https://github.com/kaizhelam/stars-animation-effect/): 
- [CodePen: Stars Animation](https://codepen.io/sarazond/pen/LYGbwj)

