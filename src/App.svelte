
<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { onMount } from "svelte";
  import * as d3 from "d3";

  import Medallero from "./components/Medallero.svelte";
  import DebugScroller from "./components/DebugScroller.svelte";
  import Loremipsum from "./components/Loremipsum.svelte";
  import Stars from "./components/stars.svelte";

  // timeline
  import { Timeline, TimelineElement } from 'svelte-animated-timeline';

	// import WorkIcon from '$lib/components/WorkIcon.svelte';
  

  /* Variables para la data del medallero */
  let deportistas = [];
  let filteredDeportistas = [];

  /* Variables para el scroller1 */
  let count;
  let index;
  let offset;
  let progress;
  let top = 0.1;
  let threshold = 0.5;
  let bottom = 0.9;

  /* Variables para el scroller 2 */
  let count2;
  let index2;
  let offset2;
  let progress2;
  let top2 = 0.1;
  let threshold2 = 0.5;
  let bottom2 = 0.9;

  /* Charts */
  let charts = {
    0: "lines_01.png",
    1: "lines_02.png",
    2: "lines_03.png",
  };

  let canvas, ctx;

  function drawBlochSphere(rotation = 0) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    ctx.save();
    ctx.translate(canvas.width / 2, canvas.height / 2);
    ctx.rotate(rotation);

    ctx.beginPath();
    ctx.arc(0, 0, 45, 0, Math.PI * 2);
    ctx.stroke();

    ctx.beginPath();
    ctx.ellipse(0, 0, 45, 20, 0, 0, Math.PI);
    ctx.stroke();

    ctx.save();
    ctx.setLineDash([5, 5]);
    ctx.beginPath();
    ctx.ellipse(0, 0, 45, 20, 0, Math.PI, 2 * Math.PI);
    ctx.stroke();
    ctx.restore();

    ctx.beginPath();
    ctx.ellipse(0, 0, 20, 45, 0, Math.PI / 2, 3 * Math.PI / 2);
    ctx.stroke();

    ctx.save();
    ctx.setLineDash([5, 5]);
    ctx.beginPath();
    ctx.ellipse(0, 0, 20, 45, 0, 3 * Math.PI / 2, Math.PI / 2);
    ctx.stroke();
    ctx.restore();

    ctx.beginPath();
    ctx.arc(0, 0, 3, 0, Math.PI * 2);
    ctx.fill();

    ctx.lineWidth = 3;

    ctx.strokeStyle = 'rgba(0, 0, 255, 0.3)';
    ctx.beginPath();
    ctx.moveTo(0, 0);
    ctx.lineTo(0, -45);
    ctx.stroke();

    ctx.strokeStyle = 'rgba(0, 0, 255, 0.9)';
    ctx.beginPath();
    ctx.moveTo(0, 0);
    ctx.lineTo(0, -15);
    ctx.stroke();

    ctx.restore();

    ctx.lineWidth = 1.5;

    ctx.beginPath();
    ctx.moveTo(0, 0);
    ctx.lineTo(30, -2);
    ctx.stroke();

    ctx.beginPath();
    ctx.arc(30, -2, 2, 0, Math.PI * 2);
    ctx.fill();
  }

  onMount(() => {
    d3.csv("./data/deportistas.csv", d3.autoType).then(data => {
      deportistas = data;
      filteredDeportistas = deportistas;
    });

    canvas = document.getElementById('bloch');
    ctx = canvas.getContext('2d');

    canvas.width = 100;
    canvas.height = 100;

    drawBlochSphere();

    window.addEventListener('scroll', handleScroll);
  });

  function handleScroll() {
    const rotation = window.scrollY * 0.01; // Adjust the factor as needed
    drawBlochSphere(rotation);
  }

  $: {
    // Es un observer que se ejecuta cuando cambia el valor de index
    switch (index) {
      case 0:
        filteredDeportistas = deportistas;
        break;
      case 1:
        filteredDeportistas = deportistas.filter(d => d.genero === "F");
        break;
      case 2:
        filteredDeportistas = deportistas.filter(d => d.genero === "M");
        break;
      case 3:
        filteredDeportistas = deportistas.filter(
          d => d.continente === "América",
        );
        break;
      default:
        filteredDeportistas = deportistas;
    }
    console.log(filteredDeportistas);
  }
</script>

<main>
  <Stars/>

  <section class="header">

    <h1 class="headline"> Computación Cuántica</h1>
  </section>
  <!-- <canvas id="bloch"></canvas> -->

  <section class=intro-section>
    <div class="contenido">
      <p>
        La computación cuántica es un campo de estudio que aplica los principios de la mecánica cuántica, 
        una rama de la física que describe el comportamiento de las partículas a nivel subatómico, 
        a la informática.
        A diferencia de la computación clásica, que utiliza bits que pueden estar en uno de dos estados (0 o 1), 
        la computación cuántica utiliza bits cuánticos, o qubits, que pueden existir en múltiples 
        estados a la vez.
      <p>
      <img src="public/images/quantumComputer.png" alt="">
    </div>
    <div class="contenido">
      <p>
        Los Qubits permiten a los ordenadores cuánticos procesar una gran cantidad de información simultáneamente. 
        Esto tiene el potencial de resolver problemas que son inabordables para los ordenadores clásicos, 
        abriendo nuevas posibilidades en campos como la criptografía, la optimización de sistemas complejos, la simulación 
        de materiales y medicamentos a nivel molecular, entre otros. 
        
        Sin embargo, la computación cuántica todavía está en sus primeras etapas de desarrollo y presenta muchos desafíos 
        técnicos y teóricos.
      </p>
      <img src="public/images/quantumComputer.png" alt="">
    </div>

  </section>


  {#if progress < 1}
  <DebugScroller
    index={index}
    count={count}
    offset={offset}
    progress={progress}
  />
  {/if}
  <!-- Primer scroller
  <Scroller
    top={top}
    threshold={threshold}
    bottom={bottom}
    bind:count={count}
    bind:index={index}
    bind:offset={offset}
    bind:progress={progress}
  >
    <div slot="background">
      <Medallero deportistas={filteredDeportistas} />
    </div>
    <div slot="foreground" class="foreground_container">
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index + 1}</h3>
          <p>Todos los deportistas</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index + 1}</h3>
          <p>Deportistas femeninas</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index + 1}</h3>
          <p>Deportistas masculinos</p>
        </div>
      </section>
      <section class="step_foreground">
        <div class="epi_foreground">
          <h3>Seccion {index + 1}</h3>
          <p>Deportistas americanos</p>
        </div>
      </section>
    </div>
  </Scroller>

  <div class="lorem_ipsum">
    <Loremipsum />
  </div> -->

  <!-- Segundo scroller -->
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
      <img src="/images/{charts[index2]}" alt="chart {index2}" class="charts"
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
    </div>
  </Scroller>
</main>

<div class="lorem_ipsum">
  <Loremipsum />
</div>

<style>
.header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 120px;
    margin-bottom: 120px;
    z-index: 1;
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
    font-weight:bolder;
    text-align: center;
    margin: 20px;
    background: linear-gradient(90deg,#7DEFE0, #87FF8C, #FF667A, #3D46F2);
    background-size: 200% 200%;
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    animation: gradientShift 4s cubic-bezier(0.42, 0, 0.58, 1) infinite;
    z-index: 1;
  }



  /* Estilos para el scroller */
  .foreground_container {
    pointer-events: none;
    padding-left: 50%;
  }

  .step_foreground {
    display: flex;
    justify-content: end;
    align-items: center;
    height: 100vh;
    border: 1px solid rgba(0, 0, 0, 0.4);
    color: white;
    padding: 1em;
    margin: 0 0 2em 0;
  }
  .epi_foreground {
    padding: 20px;
    max-width: 150px;
    background-color: rgba(0, 0, 0, 0.5);
  }
  .lorem_ipsum {
    margin: 100px auto;
    max-width: 740px;
  }
  .image_container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
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
  
</style>
