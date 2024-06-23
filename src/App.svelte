<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { onMount } from "svelte";
  import * as d3 from "d3";

  import Medallero from "./components/Medallero.svelte";
  import DebugScroller from "./components/DebugScroller.svelte";
  import Loremipsum from "./components/Loremipsum.svelte";
  import Stars from "./components/stars.svelte";
  // import Papa from 'papaparse';
  import Event from './components/Event.svelte';

  /* Variables para el scroller */
  let count2
  let index2
  let offset2
  let progress2
  let top2 = 0.1
  let threshold2 = 0.5
  let bottom2 = 0.9

  /* barras graf */
  let barras = {
    0: "ionAtrapadoBarras.png",
    1: "atomoNeutroBarras.png",
    2: "spinSemiconductorBarras.png",
    3: "bucleSuperconductorBarras.png",
  }

  /*Timeline*/
  let events = [];

  const loadCSV = async () => {
    try {
        const response = await fetch('/public/data/timeline.csv');
        const csvData = await response.text();
        const parsedData = Papa.parse(csvData, { header: true });
        events = parsedData.data; // Asigna los datos analizados a la variable events
    } catch (error) {
        console.error('Error al cargar y analizar el CSV:', error);
    }
};


  let charts = {
    0: "entrelazamiento1.png",
    1: "entrelazamiento2.png",
    2: "entrelazamiento3.png",
    3: "entrelazamiento4.png",
  };

  let currentIndex = 0;
  let currentImage = charts[currentIndex];

   // Function to change the image after 1 second delay
  function changeImage() {
    setTimeout(() => {
      currentIndex = (currentIndex + 1) < 4 ? currentIndex + 1 : 0;
      currentImage = charts[currentIndex];
      changeImage(); // Call the function again to continue the loop
    }, 100);
  }
 
 

  // Call the function to change the image when the component is mounted
  onMount(async() => {
    changeImage();
    await loadCSV();
  });
</script>

<main>
  
  <div class="header section">
    <h1 class="headline">Computación Cuántica</h1>
    <Stars />
  </div>

  <div class="contenido section">
    <p>
      La computación cuántica es un campo de estudio que aplica los principios
      de la mecánica cuántica, una rama de la física que describe el
      comportamiento de las partículas a nivel subatómico, a la informática. A
      diferencia de la computación clásica, que utiliza bits que pueden estar en
      uno de dos estados (0 o 1), la computación cuántica utiliza bits
      cuánticos, o qubits, que pueden existir en múltiples estados a la vez.
    </p>
    <p>
      <img src="public/images/quantumComputer.png" alt="" />
    </p>
  </div>

  <div class="contenido section">
    <p>
      Los Qubits permiten a los ordenadores cuánticos procesar una gran cantidad
      de información simultáneamente. Esto tiene el potencial de resolver
      problemas que son inabordables para los ordenadores clásicos, abriendo
      nuevas posibilidades en campos como la criptografía, la optimización de
      sistemas complejos, la simulación de materiales y medicamentos a nivel
      molecular, entre otros. Sin embargo, la computación cuántica todavía está
      en sus primeras etapas de desarrollo y presenta muchos desafíos técnicos y
      teóricos.
    </p>
  </div>

  <!-- Nueva sección sobre entrelazamiento y superposicion -->
  <section class="Superpos-section section">
    <div class="contenido">
      <h2 class = "subtitulo">Superposición</h2>
      <p>
        las partículas cuánticas son una combinación de todos los estados
        posibles. Fluctúan hasta que se observan y se miden. Una forma de
        ilustrar la diferencia entre la posición binaria y la superposición es
        imaginar una moneda. Los bits clásicos se miden "volteando la moneda" y
        obteniendo cara o cruz. Sin embargo, si fuese posible mirar una moneda y
        ver las dos caras a la vez, y todos los estados entre medias, la moneda
        estaría en una superposición.
      </p>
    </div>
  </section>
  <div class="section entrelazamiento-section">

    <div class="contexto-entrelazamiento">
      <h2 class = "subtitulo">Entrelazamiento</h2>
      <p class = "texto">
        El entrelazamiento cuántico es un fenómeno en el que dos qubits (o dos o
        más partículas cuánticas cualesquiera) se entrelazan de tal forma que el
        estado de una partícula no puede describirse independientemente del
        estado de la otra, sin importar la distancia que las separe.
      </p>
    </div>
    <div>
      <img src="/images/{currentImage}" alt="chart {0}" class="charts" />
    </div>
  </div>

  <div class="qubits ">
    <div class="contenido">
      <h2>Qubits</h2>
      <p>
        Los qubits son la unidad básica de información en la computación cuántica. A diferencia de los bits clásicos, los qubits pueden representar tanto 0 como 1 al mismo tiempo, gracias a la superposición cuántica. Este comportamiento permite a los ordenadores cuánticos procesar una gran cantidad de información simultáneamente.
      </p>
    </div>
  </div>

  <div id="cards" >
    <ul>
      <li class="card" style="--index: 1;">
          <div class="card__content">
            <h2 class="card_title">Ion Atrapado</h2>
          </div>
      </li>
      <li class="card" style="--index: 2;">
          <div class="card__content">
            <h2 class="card_title">Átomo Neutro</h2>
          </div>
      </li>
      <li class="card" style="--index: 3;">
          <div class="card__content">
            <h2 class="card_title">Spin Semiconductor</h2>
          </div>
      </li>
      <li class="card" style="--index: 4;">
        <div class="card__content">
          <h2 class="card_title">Bucle Superconductor</h2>
        </div>
      </li>
    </ul>
</div>

<div class="barras">
  <Scroller
top={top2}
threshold={threshold2}
bottom={bottom2}
bind:count={count2}
bind:index={index2}
bind:offset={offset2}
bind:progress={progress2}
>
<div slot="background" class="image_container">
  <img src="/images/{barras[index2]}" alt="chart {index2}" class="barras"
  />
</div>
<div slot="foreground" class="foreground_container">
  <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Seccion {index2 + 1}</h3>
      <p>Gráfico 1</p>
    </div>
  </section>
  <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Seccion {index2 + 1}</h3>
      <p>Gráfico 1</p>
    </div>
  </section>
  <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Seccion {index2 + 1}</h3>
      <p>Gráfico 1</p>
    </div>
  </section>
    <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Seccion {index2 + 1}</h3>
      <p>Gráfico 1</p>
    </div>
  </section>
  </div>
  </Scroller>
  </div>

  <div class="historia">
    <div class="contenido">
      <h2>Historia y evolución</h2>
      <h3>Hitos importantes en la computación cuántica</h3>
    </div>
  </div>
  <div class="timeline">
    {#each events as {name, date}, i}
        <Event {name} date={date} left={i % 2 === 0} eventID={name} />
    {/each}
</div>    
<div class="aplicacion">
  <div class="contenido">
    <h2>Aplicaciones de la computación cuántica en el machine learning</h2>
    <p>
      La computación cuántica ha emergido como una tecnología revolucionaria que promete transformar diversos campos, incluyendo el aprendizaje automático. Una de las aplicaciones más prometedoras es la codificación de datos cuánticos, la cual permite mapear datos clásicos a estados cuánticos, mejorando así el rendimiento de los modelos de aprendizaje automático.
    </p>
    <p>
      En numerosos estudios e investigaciones se han evaluado diversas técnicas de codificación de datos cuánticos. En en este caso, nos centraremos en un estudio que analiza las principales técnicas de codificación: codificación en base, codificación en ángulo y codificación en amplitud. Estas técnicas se aplicaron a varios modelos de aprendizaje automático, incluyendo Regresión Logística, K-Nearest Neighbors (KNN), Support Vector Machines (SVM) y varios métodos de ensamblado como Random Forest, LightGBM, AdaBoost y CatBoost.
    </p>
  </div>
</div>
</main>

<style>
  .texto {
    font-size: 18px;
    line-height: 1.6;
    position: relative;
    text-align: justify;
  }
  .subtitulo {
    font-size: 36px;
    margin-bottom:-10px;
    position: relative;
  }

  .charts {
    width: 50vw;
  }
  .section { /*si no usamos secciones borrar */
    scroll-snap-align: start;
    height: 100vh;
  }
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    z-index: 1;
    width: 100%;
  }

  /*  Animación color del título*/
  @keyframes gradientShift {
    0% {
      background-position: 0% 50%;
    }
    25% {
      background-position: 50% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    75% {
      background-position: 50% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }

  .headline {
    font-size: 60px;
    line-height: 1.2;
    font-weight: bolder;
    text-align: center;
    background: linear-gradient(90deg,  #CB9BFF, #3D46F2);
    background-size: 200% 200%;
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    animation: gradientShift 4s cubic-bezier(0.42, 0, 0.58, 1) infinite;
    z-index: 1;
    margin: 0;
  }

  /* Introducción */
  .contenido {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    margin: 0 auto;
    padding: 20px;
    max-width: 80%;
}

.contenido p {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: justify;
    z-index: 1;
}

.contenido img {
    max-width: 100%;
    width: 600px;
    z-index: 1;
    margin: 0 auto;
}
  /* Estilos para la sección de Superposición */
  .Superpos-section {
    /* background-color: #7DEFE0; */
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }

  .Superpos-section .contenido {
    display: grid;
    position: relative;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
    max-width: 80%;
    margin: 0 auto;
    padding: 20px;
  }

  .Superpos-section h2 {
    font-size: 36px;
    margin-bottom: 10px;
    position: relative;
    transform: translate(93%, -240%);
  }

  .Superpos-section p {
    font-size: 18px;
    line-height: 1.6;
    margin-bottom: 20px;
    position: relative;
    transform: translate(-10%, 10%);
    text-align: justify;
  }

  /* Estilos para la sección de Entrelazamiento */
  .entrelazamiento-section {
    position: relative;
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 20px;
    gap: 20px;
    max-width: 80%;
    margin: 0 auto;
  }

  .contexto-entrelazamiento {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 50%;
    margin-bottom: 20px;
  }

  /* Estilos para la sección de Qubits */
  .qubits {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
  }

  .qubits .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 800px;
  }

  .qubits h2 {
    font-size: 56px;
    margin-bottom: 10px;
    color: #CB9BFF;
  }

  .qubits p {
    font-size: 18px;
    line-height: 1.6;
    margin-bottom: 0;
  }

  .card {
    --index0: calc(var(--index) - 1); /* 0-based index */
    --reverse-index: calc(var(--numcards) - var(--index0)); /* reverse index */
    --reverse-index0: calc(var(--reverse-index) - 1); /* 0-based reverse index */
    position: relative; /* Needed for positioning sticky */
  }

  @keyframes scale {
      to {
          transform: scale(calc(1.1 - calc(0.1 * var(--reverse-index))));
      }
  }

  #cards {
      --numcards: 4;
      view-timeline-name: --cards-element-scrolls-in-body;
      position: relative; /* To ensure sticky positioning works */
  }

  .card__content {
      position: sticky;
      top: 0;
      --start-range: calc(var(--index0) / var(--numcards) * 100%);
      --end-range: calc((var(--index)) / var(--numcards) * 100%);

      animation: linear scale forwards;
      animation-timeline: --cards-element-scrolls-in-body;
      animation-range: exit-crossing var(--start-range) exit-crossing var(--end-range);
  }

  /* Basic styling for cards */
  ul {
      list-style-type: none;
      padding: 0;
  }

  li {
      margin: 20px 0;
  }

  .card__content {
      padding: 20px;
      background: #2B2B2D;
      border: 20px solid #202020;
      border-radius: 8px;
  }
  .card_title{
    color:#CB9BFF;
  }

   /* Estilos para el scroller */
  .foreground_container {
    pointer-events: none;
    padding-left: 50%;
    margin-top: 500px;
  }
  .step_foreground {
    display: flex;
    justify-content: center;
    align-items:center;
    height: 100vh;
    border: 1px solid rgba(255, 0, 0, 0.4);
    color: white;
    padding: 1em;
    margin: 0 auto;
  }
  .epi_foreground {
    max-width: 300px;
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.5);
    text-align: center; /* Alinea el texto al centro */
  }

  .image_container {
    display: flex;
    justify-content:center;
    align-items: center;
    height: 100vh;
  }
  .barras{
    width: 40vw; /* Ajusta el ancho como prefieras, porcentaje o valor absoluto */
    max-width: 100%;
  }

  /* Estilos para la sección de historia */
  .historia {
    margin-top: 350vh;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
  }

  .historia .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 800px;
  }

  .historia h2 {
    font-size: 56px;
    margin: 0;
  }

  .historia h3 {
    font-size: 26px;
    margin: 0;

  }

  /*Estilos del timeline*/
  .timeline {
        position: relative;
        max-width: 1200px;
        margin: 0 auto;
    }

    .timeline::after {
        content: '';
        position: absolute;
        width: 3px;
        background-color: #D9D9D9;
        top: 0;
        bottom: 0;
        left: 50%;
        margin-left: -3px;
    }

    @media screen and (max-width: 600px) {
        .timeline::after {
            left: 31px;
        }
    }

  /*Estilos para la sección de aplicación*/
   
  .aplicacion {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
  }

  .aplicacion .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 800px;
  }

  .aplicacion h2 {
    font-size: 46px;
    margin-bottom: 10px;
    color: #ffffff;
  }

  .aplicacion p {
    font-size: 18px;
    line-height: 1.6;
    margin-bottom: 0;
  }

</style>
  

