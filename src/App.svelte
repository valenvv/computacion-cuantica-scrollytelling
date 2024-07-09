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
    0: "spinSemiconductorBarras.svg",
    1: "ionAtrapadoBarras.svg",
    2: "atomoNeutroBarras.svg",
    3: "bucleSuperconductorBarras.svg",
  }

  /* Variables para el scroller */
  let count3
  let index3
  let offset3
  let progress3
  let top3 = 0.1
  let threshold3 = 0.5
  let bottom3 = 0.9

  /* barras graf */
  let graficoApp = {
    0: "KNN1.png",
    1: "SVM1.png",
    2: "Logistic Reg1.png",
    3: "AdaBoost1.png",
    4: "CatBoost1.png",
    5: "AdaBoost1.png",
    6: "LightGBM1.png",
    7: "RandomForest1.png"
  }

  /* Variables para el scroller del mapa */
  let count4
  let index4
  let offset4
  let progress4
  let top4 = 0.1
  let threshold4 = 0.5
  let bottom4 = 0.9

  /* Mapa */
  let mapa = {
    0: "world 1.svg",
    1: "world 2.svg",
    2: "world 3.svg",
    3: "world 4.svg"
  }
  const events = [
  {
    name: "La Hipótesis Cuántica",
    date: "1900",
    description: "Planck propuso que la energía se emite en paquetes discretos llamados cuantos, lo que explicó la radiación de cuerpo negro y marcó el inicio de la mecánica cuántica.",
    author: "Max Planck",
    left: true,
    eventID: "evento1"
  },
  {
    name: "El Efecto Fotoeléctrico",
    date: "1905",
    description: "Einstein explicó el efecto fotoeléctrico diciendo que la luz está hecha de fotones, que son partículas con energía proporcional a su frecuencia, apoyando así la teoría cuántica de Planck.",
    author: "Albert Einstein",
    left: false,
    eventID: "evento2"
  },
  {
    name: "El Modelo Atómico de Bohr",
    date: "1913",
    description:"Bohr propuso que los electrones orbitan el núcleo en niveles de energía específicos y pueden saltar entre estos niveles al absorber o emitir luz.",
    author: "Niels Bohr",
    left: true,
    eventID: "evento3"
  },
  {
    name: "El Principio de Incertidumbre",
    date: "1927",
    description: "Heisenberg formuló el principio de incertidumbre, que dice que es imposible medir con exactitud tanto la posición como la velocidad de una partícula al mismo tiempo.",
    author: "Werner Heisenberg",
    left: false,
    eventID: "evento4"
  },
  {
    name: "Paradoja de Einstein-Podolsky-Rosen (EPR)",
    date: "1935",
    description: "La paradoja EPR mostró que, por el entrelazamiento, el cambio en el estado de una partícula afecta instantáneamente a otra, sin importar la distancia entre ellas, cuestionando así la mecánica cuántica.",
    author: "Albert Einstein Boris Podolsky y Nathan Rosen",
    left: true,
    eventID: "evento5"
  },
  {
    name: "Desigualdades de Bell",
    date: "1964",
    description: "John Bell desarrolló pruebas que mostraron cómo las partículas entrelazadas están conectadas de manera especial comprobando la existencia del entrelazamiento, lo que es esencial para la tecnología cuántica.",
    author: "John Bell",
    left: false,
    eventID: "evento6"
  },
  {
    name: "Las Máquinas de Turing Cuánticas",
    date: "1982",
    description: "El artículo introdujo un modelo cuántico de máquina de Turing, demostrando que los sistemas cuánticos pueden realizar cálculos como las máquinas de Turing clásicas.",
    author: "Paul Benioff",
    left: true,
    eventID: "evento9"
  },
  {
    name: "Computadora Cuántica Universal",
    date: "1985",
    description: " Introdujo la idea de una computadora cuántica universal para explicar cómo podrían funcionar estas computadoras. Esto fue fundamental para el desarrollo de algoritmos cuánticos.",
    author: "David Deutsch",
    left: false,
    eventID: "evento10"
  },
  {
    name: "Algoritmo de Shor",
    date: "1994",
    description: "Es el primer algoritmo diseñado para computadoras cuánticas. Puede factorizar números grandes de manera rápida, algo difícil para las computadoras tradicionales. Esto es importante para la seguridad informatica, ya que muchos métodos de encriptación podrían volverse vulnerables.",
    author: "Peter Shor",
    left: true,
    eventID: "evento11"
  },
  {
    name: "Recocido Cuántico",
    date: "2011",
    description: "Afirmaron haber creado la primera computadora cuántica comercial, la D-Wave One, usando el recocido cuántico para resolver problemas de optimización. Hubo debate sobre si realmente ofrecía una ventaja significativa sobre las computadoras clásicas.",
    author: "Compañía canadiense D-Wave Systems",
    left: false,
    eventID: "evento13"
  },
  {
    name: "Supremacía Cuántica de Google",
    date: "2019",
    description: "La computadora cuántica de Google resolvió un problema en solo 200 segundos que una supercomputadora clásica necesitaría unos 10,000 años para resolver. Esto muestra que las computadoras cuánticas pueden ser mucho más rápidas en ciertas tareas que las computadoras tradicionales.",
    author: "Google",
    left: true,
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
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Electrolize&display=swap" rel="stylesheet">
  
  <div class="header section">
    <h1 class="headline">Computación Cuántica</h1>
    <h2 class="sub_principio">Un viaje a través de los datos</h2>
    <h2 class="sub_principioNombres">Valentina Vitetta y Caterina Villegas</h2>
    <Stars />
  </div>

  <div class="introduccion section">
    <p>
      La computación cuántica es un campo de estudio que aplica los principios
      de la mecánica cuántica, una rama de la física que describe el
      comportamiento de las partículas a nivel subatómico, a la informática. A
      diferencia de la computación clásica, que utiliza bits que pueden estar en
      uno de dos estados (0 o 1), la computación cuántica utiliza bits
      cuánticos, o qubits, que pueden existir en múltiples estados a la vez.
    </p>
    
    <img src="public/images/quantumComputer.png" alt="quantumComputer" />
    
  </div>


  <!-- Nueva sección sobre entrelazamiento y superposicion -->
  <section class="Superpos-section section">
    <div>
      <img src="/images/superposition.gif" alt="superposition"  class="charts" />
    </div>
    <div class="contenido">
      <h2 class = "subtitulo">Superposición</h2>
      <p class = "texto">
        En la superposición, los qubits pueden representar una combinación de todos los posibles estados al mismo tiempo. 
        Es como si una moneda estuviera en un estado de "cara y cruz simultáneamente", junto con todos los estados intermedios posibles. 
        Esto contrasta con la computación clásica, donde se obtiene un resultado definido al medir (como cara o cruz) al "voltear la moneda".
      </p>
    </div>
  </section>
  <div class="section entrelazamiento-section">

    <div class="contexto-entrelazamiento">
      <h2 class = "subtitulo">Entrelazamiento</h2>
      <p class = "texto">
        El entrelazamiento cuántico describe cómo dos qubits pueden estar tan interconectados que el estado de uno no puede describirse
        independientemente del estado del otro, sin importar la distancia que los separe. Este fenómeno es fundamental en la computación cuántica,
        permitiendo conexiones instantáneas que desafían las limitaciones de la física clásica.
      </p>
    </div>
    <div>
      <img src="/images/{currentImage}" alt="chart {0}" class="charts" />
    </div>
  </div>

  <div class="qubits ">
    <div class="contenido">
      <h2 data-aos="fade-up" data-aos-anchor-placement="top-center">Qubit: La unidad básica de información</h2>
      <p >
        Los qubits son la unidad básica de información en la computación cuántica. A diferencia de los bits clásicos, 
        los qubits pueden representar tanto 0 como 1 al mismo tiempo, gracias a la superposición cuántica. 
        A continuación, se describen los diferentes tipos de qubits utilizados en esta disciplina:
        
      </p>
    </div>
  </div>

  <div id="cards" >
    <ul>
      <li class="card" style="--index: 1;">
          <div class="card__content">
            <h2 class="card_title">Ion Atrapado</h2>
            <p> Son partículas atómicas cargadas que se manipulan usando campos electromagnéticos. Destacan por su estabilidad y alta temperatura de operación. Sin embargo, su desventaja principal es el tiempo necesario para manipular sus estados. </p>
            <img src="public\images\trapped Ion.png" alt="Ion atrapado" class="ion-atrapado">
          </div>
      </li>
      <li class="card" style="--index: 2;">
          <div class="card__content">
            <h2 class="card_title">Átomo Neutro</h2>
            <p>
              Son átomos individuales que se enfrían y atrapan en campos generados por láseres. Se destacan por su potencial escalabilidad y por la posibilidad de controlar individualmente cada qubit. Sin embargo, enfrentan desafíos como mantener muy bajas temperaturas para su funcionalidad y la complejidad de los sistemas de control.
            </p>
            <img src="public\images\atomo neutro.png" alt="Atomo neutro" class="atomo-neutro">
          </div>
      </li>
      <li class="card" style="--index: 3;">
          <div class="card__content">
            <h2 class="card_title">Spin Semiconductor</h2>
            <p>
              Estos qubits utilizan una propiedad cuántica llamada espín, similar a un "interruptor" que puede 
              estar en dos posiciones diferentes. Se encuentran en materiales semiconductores, controlados por 
              microondas o campos magnéticos. Se destacan por sus largos tiempos de estabilidad. Sin embargo, controlar el entorno del espín es considerado un
              desafío.
            </p>
            <img src="public\images\Spin Semiconductor.png" alt="Spin Semiconductor" class="spin-semiconductor">
          </div>
      </li>
      <li class="card" style="--index: 4;">
        <div class="card__content">
          <h2 class="card_title">Bucle Superconductor</h2>
          <p>Utilizan circuitos hechos de materiales superconductores que conducen electricidad sin resistencia a bajas temperaturas. Los estados cuánticos se representan mediante diferentes estados de corriente en el bucle. Se destacan por su tiempo de estabilidad prolongados y compatibilidad con la tecnología de circuitos superconductores. Desafíos incluyen mantener temperaturas extremadamente bajas y la complejidad en los sistemas de control.</p>

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
<div class="mapaSection">
  <div class="contenido">
    <h2>Panorama Global: Investigación en Computación Cuántica</h2>
    <p>La investigación en computación cuántica está en constante crecimiento y expansión alrededor del mundo. Este mapa muestra un panorama global de las publicaciones en este campo, destacando los países líderes en investigación cuántica.</p>
  </div>
</div>
  <div class="mapa">
    <Scroller
      top={top4}
      threshold={threshold4}
      bottom={bottom4}
      bind:count={count4}
      bind:index={index4}
      bind:offset={offset4}
      bind:progress={progress4}
    >
      <div slot="background" class="image_containerm">
        <img src="/images/{mapa[index4]}" alt="chart {index4}" class="mapa" width="55%" />
        <br>
      </div>
      <div slot="foreground" class="foreground_containerm">
        <section class="step_foregroundm">
          <div class="epi_foregroundm">
            <p> Estados Unidos y China lideran en el número total de publicaciones en computación cuántica y algoritmos cuánticos. </p>
          </div>
        </section>
        <section class="step_foregroundm">
          <div class="epi_foregroundm">
            <p>Canadá, Alemania y Rusia se destacan con una presencia notable en la investigación de computación cuántica, aunque no tan masiva como los líderes mundiales.</p>
          </div>
        </section>
        <section class="step_foregroundm">
          <div class="epi_foregroundm">
            <p>
              Países como España y Japón también tienen un impacto considerable, aunque más modesto, en este ámbito, contribuyendo significativamente al progreso global.
            </p>
          </div>
        </section>
        <section class="step_foregroundm">
          <div class="epi_foregroundm">
            <p>tiempo de cómputo</p>
          </div>
        </section>
        
      </div>
    </Scroller>
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
    <!-- <iframe title="[ Insert title here ]" aria-label="Grouped Columns" id="datawrapper-chart-7wlDE" src="https://datawrapper.dwcdn.net/7wlDE/7/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="369" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r=0;r<e.length;r++)if(e[r].contentWindow===a.source){var i=a.data["datawrapper-height"][t]+"px";e[r].style.height=i}}}))}();</script> -->
  </div>
  <div class="graficoApp">
    <Scroller
      top={top3}
      threshold={threshold3}
      bottom={bottom3}
      bind:count={count3}
      bind:index={index3}
      bind:offset={offset3}
      bind:progress={progress3}
    >
      <div slot="background" class="image_container">
        <img src="/images/{graficoApp[index3]}" alt="chart {index3}" class="graficoApp" width="50%" />
      </div>
      <div slot="foreground" class="foreground_container">
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>Presentación</h3>
            <p> Este gráfico presenta una comparación entre distintos modelos en sus versiones clásicas y cuánticas. El objetivo es visualizar las diferencias en su desempeño bajo las mismas condiciones experimentales. 
              <p>Rosa: modelos clásicos. Naranja: modelos cuánticos.</p>
              <p>Modelo actual: KNN1</p>
            
          </div>
        </section>
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>¿Qué significan los modelos?</h3>
            <p>Cada uno de estos modelos/algoritmos es una herramienta matemática que aprende patrones a partir de datos de entrenamiento. Una vez entrenados, estos modelos pueden hacer predicciones o tomar decisiones sobre nuevos datos basándose en los patrones que han aprendido.</p>
          </div>
        </section>
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>¿Qué medimos?</h3>
            <p>precisión</p>
            <p>
              Medimos el rendimiento de los dos tipos de modelos durante el proceso de entrenamiento.
              La precisión nos indica qué tan bien predice el modelo. Es una medida de la exactitud de las predicciones hechas por el modelo en comparación con los valores reales.
            </p>
          </div>
        </section>
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>¿Qué medimos?</h3>
            <p>tiempo de cómputo</p>
            <p>El tiempo de cómputo indica cuánto tiempo tarda el modelo en completar el proceso de entrenamiento. Esto es importante porque nos ayuda a evaluar la eficiencia del modelo en términos de recursos y tiempo necesarios para entrenarlo. Un menor tiempo de cómputo puede ser preferible si necesitamos resultados rápidos o si estamos trabajando con recursos limitados.
          </p>
          </div>
        </section>
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>Sección {index3 + 1}</h3>
            <p>Gráfico5</p>
          </div>
        </section>
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>Sección {index3 + 1}</h3>
            <p>Gráfico6</p>
          </div>
        </section>
        <section class="step_foreground">
          <div class="epi_foreground">
            <h3>Conclusiones</h3>
            <p>Los modelos cuánticos, en general, muestran una mayor precisión que los modelos clásicos, lo que demuestra el potencial de la computación cuántica para mejorar el rendimiento de los modelos de aprendizaje automático.</p>
            <p>Sin embargo, esta mejora en la precisión viene con un aumento en el tiempo de ejecución, lo cual es un trade-off que debe considerarse dependiendo del caso de uso específico.</p>
          </div>
        </section>
        
      </div>
    </Scroller>
  </div>
  

<div class="desafios">
  <div class="contenido">
    <h2>Desafíos actuales y futuro de la computación cuántica</h2>
    <p>
      La computación cuántica enfrenta desafíos técnicos significativos que deben ser superados para alcanzar su pleno potencial. 
    </p>
    
    <!-- <div class="wrapper">
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
      </div>  -->

      <div class="lista-desafios">
        <div class="desafio">
          <div class="numero">1</div>
          <div class="contenido">
            <h3>Decoherencia</h3>
            <p>textito</p>
          </div>
        </div>
        <div class="desafio">
          <div class="numero">2</div>
          <div class="contenido">
            <h3>Errores cuanticos</h3>
            <p>textito</p>
          </div>
        </div>
        <div class="desafio">
          <div class="numero">3</div>
          <div class="contenido">
            <h3>Escalabilidad</h3>
            <p>textito</p>
          </div>
        </div>
      </div>
      
  </div>
  </div>
  </div>

  
</main>

<style>
  .texto {
    font-weight: 200;
    line-height: 1.6;
    position: relative;
    text-align: left;
    margin-top: 0.5em;
  }
  .subtitulo {
    font-size: 36px;
    margin-bottom: 0;
    position: relative;
    text-align: left;
  }

  .charts {
    width: 40vw;
  }
  .section { /*si no usamos secciones borrar */
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    margin: 0 auto;
    padding: 20px;
    max-width: 80%;
  }
  
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    z-index: 1;
    width: 100%;
    margin-bottom: 210px;
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
    font-family: "Arp", sans-serif;
    font-weight: bolder;
    font-size: 55px;
    line-height: 1.2;
    font-weight: bolder;
    text-align: center;
    align-items: center;
    background: linear-gradient(90deg,  #CB9BFF, #3D46F2);
    background-size: 200% 200%;
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    animation: gradientShift 4s cubic-bezier(0.42, 0, 0.58, 1) infinite;
    z-index: 1;
    margin: 210px 0 0 0;
  }

  .sub_principio{
    
    font-weight: normal;
    text-align: center;
    justify-content: center;
    position: relative;
    margin: 0;
    z-index: 1;
  }

  .sub_principioNombres{
    font-weight: lighter;
    font-size: medium;
    text-align: center;
    justify-content: center;
    position: relative;
    margin-top: 0;
    z-index: 1;
  }

  /* Introducción */
  .introduccion {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 50px;
    margin: 0px auto;
    padding: 10px;
    max-width: 80%;
}

  /* Estilo para contenido de texto */
  .introduccion p {
      text-align: left;
      margin: 0;
      font-weight: 200;

  }

  /* Imagen dentro de la introducción */
  .introduccion img {
      max-width: 40%;
      width: 100px;
      margin: 0 auto;
      border-radius: 50px;
  }

  .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: left;
  }

.contenido p {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: left;
    z-index: 1;
}


/* Imagen dentro de la grilla */
.section img {
    max-width: 100%;
    width: 600px;
    margin: 0 auto;
}

.Superpos-section img{
  max-width: 70%;
  width:400px;
}

/* Estilo para los párrafos */
.section p {
  text-align: left;
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
    font-weight: 200;

  }

  .qubits h2 {
    font-size: 46px;
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
    margin: 0 auto;
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
      font-weight: 200;
  }
  .ion-atrapado {
    margin-bottom: 10px;
  }

  ul {
      list-style-type: none;
      padding: 0;
  }

  li {
      margin: 00px 0;

  }

  .card__content {
      padding: 20px 70px;
      background: #2B2B2D;
      border: 40px solid #202020;
      border-radius: 8px;
      max-width: max-content;
  }
  .card_title{
    color:#CB9BFF;
    font-weight: 750;
    font-size: 30px;
    font-family: 'Arp';
  }

 
  /* Estilos para el scroller */
  .graficoApp {
  position: relative;
  width: 80%;
}
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
    transform: translateX(30%);
    padding: 20px;
    max-width: 400px;
    background-color: rgba(125, 125, 125, 0.5);
    font-weight: 200;
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
    height: 60vh;
    text-align: center;
    margin-top: 200px;
    
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
    margin: 20px;

  }

  /*Estilos del timeline*/
  .timeline {
        position: relative;
        max-width: 1200px;
        margin: 0 auto;
        font-weight: 200;
    }

    .timeline::after {
        content: '';
        position: absolute;
        width: 3px;
        background-color: #ffffff;
        top: 4%;
        bottom:4%;
        left: 50%;
        margin-left: -3px;
        z-index: 8;
    }
    .timeline .events .date {
        font-family: 'Noto Sans', sans-serif; /* Cambia 'Noto Sans' por la fuente que desees utilizar */
        /* Otros estilos aquí si los necesitas */
    }

    @media screen and (max-width: 600px) {
        .timeline::after {
            left: 31px;
        }
    }

  /*Estilos para la sección de desafios*/

  .aplicacion {
  margin-top: 200px; /*Adapt fondo*/
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
  font-weight: 200;
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
      margin-top: 360px; /*Adapt fondo*/
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
      font-weight: 200;
    }

    .desafios h2 {
      font-size: 46px;
      margin-bottom: 10px;
      color: #BB8DF5;
    }

    .desafios p {
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
     
  main{
    background-image: url("images/fondo3.png");
    background-size: 100vw;
    margin: 0 0;
    z-index: 2;
  }


  /*Estilos para los desafíos*/
  .lista-desafios {
  display: flex;
  flex-direction: column;
  gap: 20px;
  }

  .desafio {
    display: flex;
    align-items: center;
    gap: 15px;
  }

  .numero {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: #4f138f; /* Color del fondo del círculo */
    color: white; /* Color del texto del número */
    font-size: 1.5em;
  }

  .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center; /* Centra el contenido verticalmente */
  }

  .contenido h3 {
    margin: 0;
    align-self: flex-start; /* Asegura que el h3 esté alineado a la izquierda */
  }

  .contenido p {
    margin: 5px 0 0 0;
  }

  /*Estilos scroller mapa*/
  .mapaSection {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 60vh;
    text-align: center;
    margin-top: 200px;
    
  }
  .mapaSection .contenido {
    max-width: 800px;
    font-weight: 200;

  }

  .mapaSection h2 {
    font-size: 46px;
    margin-bottom: 10px;
    color: #ff9d42;
  }

  .mapa {
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .mapa p {
    margin-bottom: 0;
    justify-content:left;
    align-items: center;
    font-weight: 200;
  }

  .image_containerm{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 90vh;
  }
  .foreground_containerm {
    align-items: center;
  }
  .step_foregroundm {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 90vh;
    color: white;
    padding: 1em;
    margin: 0 0 10em 0;
  }
  .epi_foregroundm {
    padding: 20px;
    max-width: 120px;
    background-color: rgba(0, 0, 0, 0.877);
  }

  
</style>
  

