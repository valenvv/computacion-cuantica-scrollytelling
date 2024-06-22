<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { onMount } from "svelte";
  import * as d3 from "d3";

  import Medallero from "./components/Medallero.svelte";
  import DebugScroller from "./components/DebugScroller.svelte";
  import Loremipsum from "./components/Loremipsum.svelte";
  import Stars from "./components/stars.svelte";

  // timeline
  import { Timeline, TimelineElement } from "svelte-animated-timeline";

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
    }, 60);
  }

  // Call the function to change the image when the component is mounted
  onMount(() => {
    changeImage();
  });
</script>

<main>
  
  <div class="header section">
    <h1 class="headline">Computación Cuántica</h1>
    <Stars />
  </div>
  <!-- <canvas id="bloch"></canvas> -->

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
    <!-- <Medallero/> -->
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
</main>

<div class="lorem_ipsum section">
  <Loremipsum />
</div>

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

  /* Estilos para la sección de Entrelazamiento */
  .entrelazamiento-section {
    position: relative;
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .contexto-entrelazamiento {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 50vw;
    margin-bottom: 20px;
  }
  .section {
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
    background: linear-gradient(90deg, #7defe0, #87ff8c, #ff667a, #3d46f2);
    background-size: 200% 200%;
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    animation: gradientShift 4s cubic-bezier(0.42, 0, 0.58, 1) infinite;
    z-index: 1;
    margin: 0;
  }

  /* Introducción */
  .intro-section {
    display: flex;
    flex-direction: column;
    padding: 50px 20px;
    /*background: #1e1e1e;*/
    margin: 20px 0;
    z-index: 2;
  }

  .contenido {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
    z-index: 2;
  }

  .contenido p {
    display: flex;
    flex-direction: column;
    justify-content: center;
    z-index: 1;
  }

  .contenido img {
    max-width: 100%;
    width: 600px;
    z-index: 1;
  }
  /* Estilos para la sección de Superposición */
  .Superpos-section {
    /* background-color: #7DEFE0; */
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .Superpos-section .contenido {
    display: grid;
    position: relative;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
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
  }
</style>
