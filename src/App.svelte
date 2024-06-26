<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { onMount } from "svelte";
  import * as d3 from "d3";
  import DebugScroller from "./components/DebugScroller.svelte";
  import Stars from "./components/stars.svelte";
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


  const events = [
  {
    name: "La Hipótesis Cuántica",
    date: "1900",
    description: "Max Planck (físico teórico alemán), introdujo el concepto de niveles de energía cuantificada para explicar el fenómeno de la radiación de cuerpo negro. Propuso que la energía no se emite de manera continua, sino en paquetes discretos llamados cuantos. Esto marcó el comienzo de una nueva era en la física y marcó las bases para el desarrollo de la mecánica cuántica.",
    author: "Max Planck",
    left: true,
    eventID: "evento1"
  },
  {
    name: "El Efecto Fotoeléctrico",
    date: "1905",
    description: "Albert Einstein publicó un estudio sobre el efecto fotoeléctrico, en el cual explicó que la luz está compuesta por partículas denominadas fotones. Cada uno de estos fotones porta una cantidad de energía discreta, la cual es proporcional a su frecuencia. Su análisis reforzó la hipótesis cuántica propuesta por Planck, y contribuyó significativamente a la creciente comprensión del comportamiento de la luz, similar al de las partículas.",
    author: "Albert Einstein",
    left: false,
    eventID: "evento2"
  },
  {
    name: "El Modelo Atómico de Bohr",
    date: "1913",
    description: "Desarrollo del modelo atómico de Bohr, en el cual se propuso que los electrones orbitan el núcleo en niveles de energía cuantizados. Este modelo proporcionó una comprensión más profunda de la estructura atómica y la naturaleza cuantizada de la energía. También introdujo el concepto de saltos cuánticos, donde los electrones podrían moverse entre niveles de energía al absorber o emitir fotones, demostrando aún más la importancia de la cuantización en los sistemas atómicos.",
    author: "Niels Bohr",
    left: true,
    eventID: "evento3"
  },
  {
    name: "El Principio de Incertidumbre",
    date: "1927",
    description: "Werner Heisenberg, un físico alemán, formuló el principio de incertidumbre, un concepto fundamental en la mecánica cuántica. El principio establece que es imposible conocer simultáneamente tanto la posición como el momento de una partícula con perfecta precisión. Esto destacó las limitaciones inherentes en la medición de sistemas cuánticos.",
    author: "Werner Heisenberg",
    left: false,
    eventID: "evento4"
  },
  {
    name: "Paradoja de Einstein-Podolsky-Rosen (EPR)",
    date: "1935",
    description: "Artículo introduciendo la paradoja EPR, que cuestionaba la completitud de la mecánica cuántica debido al fenómeno del entrelazamiento. El entrelazamiento implica que las propiedades de dos o más partículas pueden estar correlacionadas de tal manera que el estado de una partícula afecta instantáneamente el estado de la otra, independientemente de la distancia entre ellas.",
    author: "Albert Einstein Boris Podolsky y Nathan Rosen",
    left: true,
    eventID: "evento5"
  },
  {
    name: "Desigualdades de Bell",
    date: "1964",
    description: "El físico John Bell formuló las desigualdades de Bell, que proporcionaron una forma de probar experimentalmente la validez de la paradoja EPR. La violación de las desigualdades de Bell en experimentos posteriores confirmó la existencia del entrelazamiento, un recurso clave para la computación cuántica.",
    author: "John Bell",
    left: false,
    eventID: "evento6"
  },
  {
    name: "Primera Conferencia sobre Física y Computación (PhysComp)",
    date: "1980",
    description: "Este encuentro interdisciplinario facilitó el intercambio de ideas y la exploración de enfoques novedosos para la computación cuántica, lo que finalmente llevó al surgimiento del campo tal como lo conocemos hoy. La conferencia PhysComp demostró el creciente interés y reconocimiento del potencial impacto de la mecánica cuántica en la computación y el procesamiento de información.",
    author: "",
    left: true,
    eventID: "evento7"
  },
  {
    name: "Propuesta de Richard Feynman sobre las Computadoras Cuánticas",
    date: "1981",
    description: "El físico Richard Feynman dio una conferencia seminal en la Primera Conferencia sobre la Física de la Computación, proponiendo que una computadora que opera según los principios cuánticos podría simular eficientemente sistemas cuánticos. La perspicacia de Feynman fue crucial ya que destacó las limitaciones de las computadoras clásicas en la simulación de fenómenos cuánticos.",
    author: "Richard Feynman",
    left: false,
    eventID: "evento8"
  },
  {
    name: "Las Máquinas de Turing Cuánticas",
    date: "1982",
    description: "Artículo describiendo un modelo mecánico cuántico de una máquina de Turing. Este modelo, marco las bases para los modelos de computación cuántica al demostrar que los principios de la mecánica cuántica podían aplicarse a los fundamentos teóricos de la computación. Este trabajo mostró que los sistemas cuánticos podrían utilizarse para realizar cálculos de una manera análoga a las máquinas de Turing clásicas.",
    author: "Paul Benioff",
    left: true,
    eventID: "evento9"
  },
  {
    name: "Computadora Cuántica Universal",
    date: "1985",
    description: "Artículo que introdujo el concepto de una computadora cuántica universal. Deutsch se basó en las ideas de Feynman y Benioff, y proporcionó un marco más concreto para entender cómo podrían operar las computadoras cuánticas. Este trabajo marco las bases para el desarrollo de algoritmos cuánticos.",
    author: "David Deutsch",
    left: false,
    eventID: "evento10"
  },
  {
    name: "Algoritmo de Shor",
    date: "1994",
    description: "Es el primer algoritmo cuántico, conocido ahora como el algoritmo de Shor. Este algoritmo utiliza los principios de la mecánica cuántica para factorizar eficientemente números grandes, una tarea que tomaría un tiempo exponencialmente mayor en computadoras clásicas. La habilidad de factorizar números grandes tiene implicaciones significativas para la criptografía, ya que muchos esquemas de encriptación, como RSA, dependen de la dificultad de este problema para su seguridad. Demostró el potencial poder de la computación cuántica, resaltando su habilidad para resolver problemas que previamente se consideraban intratables para las computadoras clásicas.",
    author: "Peter Shor",
    left: true,
    eventID: "evento11"
  },
  {
    name: "Algoritmo de Grover",
    date: "1996",
    description: "Algoritmo cuántico que busca eficientemente en bases de datos no ordenadas. Puede buscar en una base de datos de N elementos en aproximadamente √N pasos, lo cual es mucho más rápido que los algoritmos clásicos que requieren alrededor de N pasos. Aunque no es tan rápido como el algoritmo de Shor, el algoritmo de Grover muestra cómo la computación cuántica puede ser superior a la computación clásica en ciertas tareas.",
    author: "Lov Grover",
    left: false,
    eventID: "evento12"
  },
  {
    name: "Recocido Cuántico",
    date: "2011",
    description: "Afirmaron haber construido la primera computadora cuántica comercialmente disponible, la D-Wave One. Este sistema se basaba en el recocido cuántico, un enfoque especializado de la computación cuántica que se centra en resolver problemas de optimización. Sin embargo, la aplicabilidad práctica y la verdadera naturaleza cuántica de los sistemas de D-Wave fueron objeto de debate entre los investigadores, con algunos argumentando que los sistemas proporcionaban solo una aceleración limitada en comparación con las computadoras clásicas.",
    author: "Compañía canadiense D-Wave Systems",
    left: true,
    eventID: "evento13"
  },
  {
    name: "Supremacía Cuántica de Google",
    date: "2019",
    description: "La computadora cuántica de Google resolvió un problema específico en 200 segundos que llevaría aproximadamente 10,000 años a una supercomputadora clásica. Este logro marcó la primera vez que una computadora cuántica superó a las computadoras clásicas en una tarea computacional bien definida, proporcionando una prueba de concepto para el potencial poder de la computación cuántica.",
    author: "Google",
    left: false,
    eventID: "evento14"
  }
];


  

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
  onMount(() => {
    changeImage();

    
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
      <img src="public/images/quantumComputer.jpg" alt="" />
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
    <div>
      <img src="/images/superposition.gif" alt="superposition"  class="charts" />
    </div>
    <div class="contenido">
      <h2 class = "subtitulo">Superposición</h2>
      <p class = "texto">
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
            <p>
              Son partículas atómicas cargadas que se confinan y manipulan utilizando campos electromagnéticos. Destacan por su mayor tiempo de coherencia y una temperatura de operación más alta. No obstante, su principal desventaja radica en el tiempo necesario para manipular el estado de los qubits. Empresas como Honeywell y IonQ emplean este tipo de qubits.
            </p>
            <img src="public\images\trapped Ion.png" alt="Ion atrapado" class="ion-atrapado">
          </div>
      </li>
      <li class="card" style="--index: 2;">
          <div class="card__content">
            <h2 class="card_title">Átomo Neutro</h2>
            <p>
              Se codifican en átomos individuales que se enfrían y atrapan en un potencial óptico generado por láseres cruzados. Estos átomos pueden ser manipulados y controlados mediante pulsos de láser locales. Los sistemas de átomos neutros ofrecen ventajas como la escalabilidad potencial a un gran número de qubits y la capacidad de direccionar y manipular individualmente cada qubit1. Sin embargo, también enfrentan desafíos, como la necesidad de mantener los átomos ultrafríos y la complejidad de los sistemas de control.
            </p>
            <img src="public\images\atomo neutro.png" alt="Atomo neutro" class="atomo-neutro">
          </div>
      </li>
      <li class="card" style="--index: 3;">
          <div class="card__content">
            <h2 class="card_title">Spin Semiconductor</h2>
            <p>usan una propiedad cuántica llamada espín, que puede ser como un “interruptor” que está en posición |0⟩ o |1⟩.

              Estos qubits se encuentran en materiales semiconductores, donde los electrones están atrapados en un lugar pequeño. Para controlar estos qubits, se usan microondas o campos magnéticos.
              
              Las ventajas incluyen que pueden usar la tecnología de los semiconductores que ya existe y que pueden mantener su estado cuántico por mucho tiempo. Sin embargo, es difícil controlar el entorno del espín y reducir el ruido.
            </p>
            <img src="public\images\Spin Semiconductor.png" alt="Spin Semiconductor" class="spin-semiconductor">
          </div>
      </li>
      <li class="card" style="--index: 4;">
        <div class="card__content">
          <h2 class="card_title">Bucle Superconductor</h2>
          <p>utilizan circuitos hechos de materiales superconductores, que pueden conducir electricidad sin resistencia cuando se enfrían a temperaturas muy bajas. Una corriente eléctrica puede circular por un bucle superconductor indefinidamente sin perder energía. Los estados cuánticos se representan mediante diferentes estados de corriente en el bucle.</p>
          <p>Las ventajas de los qubits de bucles superconductores incluyen tiempos de coherencia relativamente largos y la capacidad de integrarse con la tecnología de circuitos superconductores existente. Sin embargo, también enfrentan desafíos, como la necesidad de mantener temperaturas extremadamente bajas y la complejidad de los sistemas de control</p>
          <img src="public\images\Bucles Superconductores.png" alt="bucle superconductor" class="bucle-super">
        </div>
      </li>
    </ul>
</div>

<div class="qubits">
  <div class="contenido">
    <p> La capacidad de entrelazar múltiples qubits simultáneamente es crucial para el rendimiento y la potencia de los sistemas cuánticos. Cuantos más qubits se puedan entrelazar simultáneamente, mayor será la capacidad del sistema para resolver problemas complejos y realizar cálculos que están fuera del alcance de las computadoras clásicas. Por lo tanto, la cantidad de qubits que se pueden entrelazar es un indicador clave del potencial y la escalabilidad de una tecnología de qubits.</p>
    <p>A continuación, se presenta una comparación de la cantidad de qubits que se pueden entrelazar simultáneamente en diferentes sistemas de qubits:</p>
  </div>
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
<div slot="background" class="image_container" >
  <img src="/images/{barras[index2]}" alt="chart {index2}" class="barras" width="50%"
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
      <p>Gráfico 2</p>
    </div>
  </section>
  <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Seccion {index2 + 1}</h3>
      <p>Gráfico 3</p>
    </div>
  </section>
    <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Seccion {index2 + 1}</h3>
      <p>Gráfico 4</p>
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
    {#each events as {name, date,description}, i}
        <Event {name} date={date} left={i % 2 === 0} eventID={name} description={description} data-aos="slide-left"/>
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

<div class="desafios">
  <div class="contenido">
    <h2>Desafíos actuales y futuro de la computación cuántica</h2>
    <p>
      La computación cuántica enfrenta desafíos técnicos significativos que deben ser superados para alcanzar su pleno potencial. 
    </p>
    
    
    <div class="wrapper">
      <div class="container">
          <input type="radio" name="slide" id="c1" checked>
          <label for="c1" class="tarjeta">
          </label>
          <input type="radio" name="slide" id="c2" >
          <label for="c2" class="tarjeta">
          </label>
          <input type="radio" name="slide" id="c3" >
          <label for="c3" class="tarjeta">
          </label>
          <input type="radio" name="slide" id="c4" >
          <label for="c4" class="tarjeta">
          </label>
      </div>
  </div>
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
    width: 40vw;
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
    pposition: relative;
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 20px;
    gap: 20px;
    max-width: 80%;
    margin: 0 auto;
  }

  .Superpos-section .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 50%;
    margin-bottom: 20px;
  }
  
  .Superpos-section h2{
    transform: translateX(-40%); 
    /* cambiar cuando sepas como hacer que este tirado para la izq como Entrelazamiento */
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
    height: 70vh;
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
    /* background: lightgray; */
    padding: 2rem;
    border-radius: 8px;
    position: sticky;
    top: 1rem;
  }

  @keyframes scale {
      to {
          transform: scale(calc(1.1 - calc(0.1 * var(--reverse-index))));
      }
  }

  #cards {
    width: 80%;
    margin: 5% auto;
    display: grid;
      --numcards: 4;
      view-timeline-name: --cards-element-scrolls-in-body;
      gap: 1rem;
    }

  .card__content {
      position: sticky;
      --start-range: calc(var(--index0) / var(--numcards) * 100%);
      --end-range: calc((var(--index)) / var(--numcards) * 100%);

      animation: linear scale forwards;
      animation-timeline: --cards-element-scrolls-in-body;
      animation-range: exit-crossing var(--start-range) exit-crossing var(--end-range);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      margin: auto;
  }
  .ion-atrapado {
    margin-bottom: 10px;
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

  .image_container {
    display: flex;
    margin-left: 150px;
    align-items: center;
    height: 100vh;
  }


  /* Estilos para la sección de historia */
  .historia {
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

  /*Estilos para la sección de desafios*/
  
  .aplicacion {

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: auto;
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

  /*Estilos para la sección de desafios*/
  
    .desafios {

      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: auto;
      text-align: center;
    }

    .desafios .contenido {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      max-width: 800px;
    }

    .desafios h2 {
      font-size: 46px;
      margin-bottom: 10px;
      color: #BB8DF5;
    }

    .desafios p {
      font-size: 18px;
      line-height: 1.6;
      margin-bottom: 0;
    }
    /* intento de tarjetas */
    
    .wrapper {
      box-sizing: border-box;
      width: 80%;
      height: 90vh;
      display: flex;
      align-items: center;
      justify-content: center;
  }

  .container {
    
      height: 400px;
      display: flex;
      flex-wrap: nowrap;
      justify-content: center;
  }

  .tarjeta {
      width: 80px;
      border-radius: .75rem;
      background-size: cover;
      cursor: pointer;
      overflow: hidden;
      border-radius: 2rem;
      margin: 0 10px;
      display: flex;
      align-items: flex-end;
      transition: .6s cubic-bezier(.28,-0.03,0,.99);
      /* filter: grayscale(1) brightness(0.5);  */
  }

  input {
    display: none;
  }

  input:checked + label {
    width: 700px;
    /* filter: grayscale(0) brightness(1); */
  }

  input:not(:checked) + .tarjeta[for="c1"],
  input:not(:checked) + .tarjeta[for="c2"],
  input:not(:checked) + .tarjeta[for="c3"],
  input:not(:checked) + .tarjeta[for="c4"] {
    /* background: linear-gradient(to bottom, #20007A, #461DBB); */
    background: linear-gradient(to bottom, #20007A, #5439ff);
  }



  .tarjeta[for="c1"] {
    
    /* background: linear-gradient(to bottom, #2A0D39, #711D76); */
    background-image: url('public/images/deco2.png');
    background-position: center;
  }
  .tarjeta[for="c2"] {
    /* background: linear-gradient(to bottom, #20007A, #4E22CD); */
    background-image: url('public/images/erroresCuanticos2.png');
    background-position: center;
  }
  .tarjeta[for="c3"] {
    background-image: url('public/images/Escalabilidad.png');
    background-position: center; 

   }
  .tarjeta[for="c4"] {
    background: linear-gradient(to bottom, #20007A, #4E22CD);
  }
     
</style>
  

