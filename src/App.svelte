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
    3: "bucleSuperconductorBarras.svg"
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
    2: "LogisticReg1.png",
    3: "AdaBoost1.png",
    4: "CatBoost1.png",
    5: "LightGBM1.png",
    6: "RandomForest1.png"
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
 
  let cancion;
  let reproduciendo = false;
 

  // Call the function to change the image when the component is mounted
  onMount(() => {
    changeImage();
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


</script>

<main>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Electrolize&display=swap" rel="stylesheet">
  
  <div class="header section">
    <h1 class="headline">Computación Cuántica</h1>
    <h2 class="sub_principio">Un viaje a través de los datos</h2>
    <h2 class="sub_principioNombres">Valentina Vitetta y Caterina Villegas</h2>
    <div class="sub_principioPlay">
      <p>Viví la experiencia completa</p>
      <button class="play" on:click={togglePlayback}>
        <img src="../images/play.png" alt="play" width="30px">
      </button>
    </div>
    <Stars />
  </div>
  
  <audio id="cancion">
    <source src="song/cancion.mp3" type="audio/mp3">
  </audio>
  
  <div class="introduccion section">
    <p class="texto">
      La <strong>computación cuántica</strong> es un campo de estudio que aplica los principios
      de la mecánica cuántica, una rama de la física que describe el
      comportamiento de las partículas a nivel subatómico, a la informática. A
      diferencia de la computación clásica, que utiliza bits que pueden estar en
      uno de dos estados (0 o 1), la computación cuántica utiliza bits
      cuánticos, o qubits, que pueden existir en múltiples estados a la vez.
    </p>
    
    <img src="/images/quantumComputer.png" alt="quantumComputer" />
    
  </div>


  <!-- Nueva sección sobre entrelazamiento y superposicion -->
  <section class="Superpos-section section">
    <div>
      <img src="/images/superposition.gif" alt="superposition"  class="charts" />
    </div>
    <div data-aos="fade-up" class="contenido">
      <h2 class = "subtitulo">Superposición</h2>
      <p class = "texto">
        En la superposición, los qubits pueden representar una combinación de todos los posibles estados al mismo tiempo. 
        Es como si una moneda estuviera en un estado de "cara y cruz simultáneamente", junto con todos los estados intermedios posibles. 
        Esto contrasta con la computación clásica, donde se obtiene un resultado definido al medir (como cara o cruz) al "voltear la moneda".
      </p>
    </div>
  </section>
  <div class="section entrelazamiento-section">

    <div data-aos="fade-up" class="contexto-entrelazamiento">
      <h2 class = "subtitulo">Entrelazamiento</h2>
      <p  class = "texto">
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
    <div class="circle-top1"></div> <!-- Parte superior circular con degradado -->
    <div class="contenido">
      <h2 data-aos="fade-up">Qubit: La unidad básica de información</h2>
      <p >
        A diferencia de los bits clásicos, los qubits pueden representar tanto 0 como 1 al mismo tiempo, gracias a la superposición cuántica. 
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
            <img src="/images/trapped Ion.png" alt="Ion atrapado" class="ion-atrapado">
          </div>
      </li>
      <li class="card" style="--index: 2;">
          <div class="card__content">
            <h2 class="card_title">Átomo Neutro</h2>
            <p>
              Son átomos individuales que se enfrían y atrapan en campos generados por láseres. Se destacan por su potencial escalabilidad y por la posibilidad de controlar individualmente cada qubit. Sin embargo, enfrentan desafíos como mantener muy bajas temperaturas para su funcionalidad y la complejidad de los sistemas de control.
            </p>
            <img src="/images/atomo neutro.png" alt="Atomo neutro" class="atomo-neutro">
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
            <img src="/images/Spin Semiconductor.png" alt="Spin Semiconductor" class="spin-semiconductor">
          </div>
      </li>
      <li class="card" style="--index: 4;">
        <div class="card__content">
          <h2 class="card_title">Bucle Superconductor</h2>
          <p>Utilizan circuitos hechos de materiales superconductores que conducen electricidad sin resistencia a bajas temperaturas. Los estados cuánticos se representan mediante diferentes estados de corriente en el bucle. Se destacan por su tiempo de estabilidad prolongados y compatibilidad con la tecnología de circuitos superconductores. Desafíos incluyen mantener temperaturas extremadamente bajas y la complejidad en los sistemas de control.</p>

          <img src="/images/Bucles Superconductores.png" alt="bucle superconductor" class="bucle-super">
        </div>
      </li>
    </ul>
</div>

<div class="qubits">
  <div class="contenido">
    <h2>Capacidad de entrelazamiento: Midiendo su eficiencia</h2>
    <p> La capacidad de entrelazar múltiples qubits simultáneamentees crucial para el rendimiento y la potencia de los sistemas cuánticos. Cuantos más qubits se puedan entrelazar simultáneamente, mayor será la capacidad del sistema para resolver problemas complejos y realizar cálculos que están fuera del alcance de las computadoras clásicas. </p>
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
      <h3>Spin Semiconductor</h3>
      <p>Pueden entrelazar hasta 4 qubits a la vez. Aunque este número es menor, la tecnología está en desarrollo y tiene potencial para mejoras futuras.</p>
    </div>
  </section>
  <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Ion Atrapado</h3>
      <p>Pueden entrelazar hasta 32 qubits simultáneamente, lo que demuestra una capacidad considerable para realizar cálculos cuánticos más complejos.</p>
    </div>
  </section>
  <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Átomo Neutro</h3>
      <p>Permiten entrelazar hasta 50 qubits al mismo tiempo, destacándose por su eficiencia en el control y manipulación de qubits.</p>
    </div>
  </section>
    <section class="step_foreground">
    <div class="epi_foreground">
      <h3>Bucle Superconductor</h3>
      <p>Lideran con la capacidad de entrelazar hasta 65 qubits simultáneamente, lo que los posiciona a la vanguardia de la tecnología cuántica actual.</p>
    </div>
  </section>
  </div>
  </Scroller>
  </div>

  <div class="historia">
    <div class="circle-top"></div> <!-- Parte superior circular con degradado -->
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
            <p>
              Por último, aunque algunos países tienen menos publicaciones
              en computación cuántica, su potencial no debe subestimarse.
            </p>
            <p>
              Con el tiempo y 
              el apoyo adecuado, estas naciones podrían hacer contribuciones significativas al 
              progreso global en este campo emergente. La colaboración internacional será clave para fomentar la investigación en este ámbito.
            </p>
          </div>
        </section>
        
      </div>
    </Scroller>
  </div> 
  <div class="aplicacion">
    <div class="imagen-fondo">
      <img src="public\images\firulete.png" alt="Background Image" />
    </div>
    <div class="contenido">
      <h2>Revolución cuántica en el machine learning: Datos transformados</h2>
      <p class= "parrafosAppIntro" style="margin-top: 30px; margin-bottom: 20px;"> 
        La computación cuántica está revolucionando el aprendizaje automático mediante la codificación de datos cuánticos. Esta técnica transforma datos comunes en estados cuánticos, donde un estado cuántico indica si un qubit está en 1, 0, o una combinación de ambos simultáneamente en un instante específico. Esta capacidad única permite a los algoritmos cuánticos procesar y analizar información de manera más rápida y eficiente que los métodos clásicos de aprendizaje automático. 
      </p>
      <p class= "parrafosAppIntro"  style="margin-bottom: 60px;"> 
        El siguiente gráfico presenta una comparación entre distintos modelos de aprendizaje automático en sus versiones clásicas y cuánticas. El objetivo es visualizar las diferencias en su desempeño bajo las mismas condiciones experimentales. Se analizan desde métodos lineales hasta técnicas avanzadas de ensamblado.
      </p>
      
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
        <div slot="background" class="image_containerApp">
          <img src="/images/{graficoApp[index3]}" alt="chart {index3}" class="graficoApp" width="50%" />
        </div>
        <div slot="foreground" class="foreground_containerApp">
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">Presentación</h3>
              <p class="parrafosApp"> En este gráfico, el eje x representa el tiempo de ejecución y el eje y la precisión de los modelos. Los modelos clásicos se representan con puntos de color rosa, mientras que los modelos cuánticos se representan con puntos de color naranja. 
               
                <p class= "modeloActual">Modelo actual: KNN</p>
              
            </div>
          </section>
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">¿Qué son los modelos?</h3>
              <p class="parrafosApp">Son herramientas matemáticas que aprenden patrones de datos de entrenamiento. Una vez entrenados, pueden hacer predicciones o tomar decisiones sobre nuevos datos basándose en los patrones que han aprendido.</p>
              <p class= "modeloActual">Modelo actual: SVM</p>
            </div>
          </section>
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">Modelos evaluados</h3>
              <ul class="bullets">
                <li>Regresión Logística (LogisticReg)</li>
                <li>K-Nearest Neighbors (KNN)</li>
                <li>Support Vector Machines (SVM)</li>
                <li>Random Forest</li>
                <li>LightGBM</li>
                <li>AdaBoost</li>
                <li>CatBoost</li>
              </ul>
              <p class= "modeloActual">Modelo actual: LogisticReg</p>
            </div>
          </section>
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">¿Qué medimos?</h3>
              <p>Precisión</p>
              <p class="parrafosApp">
                Durante el entrenamiento de los modelos, medimos su rendimiento. La precisión nos dice qué tan exactas son las predicciones del modelo en comparación con los valores reales.
              </p>
              <p class= "modeloActual">Modelo actual: AdaBoost</p>
            </div>
          </section>
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">¿Qué medimos?</h3>
              <p>Tiempo de ejecución (s)</p>
              <p class="parrafosApp">
                Este término se refiere al tiempo necesario para que el modelo complete el proceso de entrenamiento. Es crucial para evaluar la eficiencia del modelo en términos de recursos y tiempo utilizados durante el entrenamiento.
            </p>
            <p class= "modeloActual">Modelo actual: CatBoost</p>
            </div>
          </section>
          
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">Versión clásica vs cuántica</h3>
              <!-- <p>
                Cada modelo tiene una versión clásica y una versión cuántica. Esto significa que se desarrollaron dos variantes del mismo modelo, una adaptada para funcionar en computadoras clásicas y otra en computadoras cuántica.
              </p> -->
              <ul class="bullets">
                <li><strong>Versión Clásica:</strong> Es la implementación estándar del modelo utilizando principios tradicionales de matemáticas y computación.</li>
                <li><strong>Versión Cuántica:</strong> Es una adaptación del mismo modelo que utiliza principios de la mecánica cuántica.</li>
              </ul>
              <p class= "modeloActual">Modelo actual: LightGBM</p>
            </div>
          </section>
          <section class="step_foregroundApp">
            <div class="epi_foregroundApp">
              <h3 class="titulosApp">Conclusiones</h3>
              <p>Los modelos cuánticos suelen ser más precisos que los modelos clásicos, mostrando así su potencial para mejorar el aprendizaje automático. </p>
              <p>Sin embargo, esta mejora viene con un aumento en el tiempo de ejecución, lo cual es un trade-off que debe considerarse dependiendo del caso de uso.</p>
              <p class= "modeloActual">Modelo actual: RandomForest</p>
            </div>
          </section>
          
        </div>
      </Scroller>
    </div>
    
  
  <div class="desafios">
    <div class="imagen-fondo1">
      <img src="public\images\firulete1.png" alt="Background Image" />
    </div>
    <div class="contenido">
      <h2>Desafíos actuales y futuro de la computación cuántica</h2>
      <!-- <p>
        La computación cuántica enfrenta desafíos técnicos significativos que deben ser superados para alcanzar su pleno potencial. 
      </p> -->
      
        <div class="lista-desafios">
          <div class="desafio">
            <div class="numero">1</div>
            <div class="contenido">
              <h3 class= "titulosDesafios">Decoherencia</h3>
              <p>
                Los qubits pueden perder su estado cuántico cuando interactúan con el entorno.</p>
            </div>
          </div>
          <div class="desafio">
            <div class="numero">2</div>
            <div class="contenido">
              <h3 class= "titulosDesafios">Errores cuanticos</h3>
              <p>Los errores en los qubits, al ser sensibles al entorno, limitan la exactitud de los sistemas cuánticos.</p>
            </div>
          </div>
          <div class="desafio">
            <div class="numero">3</div>
            <div class="contenido">
              <h3 class= "titulosDesafios">Escalabilidad</h3>
              <p>Mantener la precisión y coherencia de múltiples qubits es un desafío por su sensibilidad al entorno.</p>
            </div>
          </div>
        </div>
        
    </div>
    </div>
    </div>
    <div class="imagen-fondo1">
      <img src="public\images\firulete2.png" alt="Background Image" />
    </div>
  <!-- Conclusion -->
  <div class="bg-animation">
    <div id="stars"></div>
    <div id="stars2"></div>
    <div id="stars3"></div>
    <div id="stars4"></div>
    <div>
      <div class="contenido">
        <h2>Conclusión</h2>
        <p>
          El viaje hacia la computación cuántica es un desafío monumental lleno de obstáculos técnicos y científicos. Sin embargo, los avances continuos y la dedicación de la comunidad científica nos acercan cada día más a un futuro donde los ordenadores cuánticos pueden resolver problemas que hoy parecen insuperables. A medida que superamos estos desafíos, nos acercamos a un mundo donde la computación cuántica se convierte en una herramienta poderosa. 
        </p>
      </div>
    </div>

  </div>

  <footer class="footer">
    <div class="container">
      <div class="row">
        <div class="footer-col">
          <h4>Visualzación de Datos | Entrega Final</h4>
          <ul>
            <li><a href="https://www.utdt.edu/">Universidad Torcuato Di Tella</a></li>
            <li><a href="https://www.utdt.edu/ver_contenido.php?id_contenido=19866&id_item_menu=31534">Licenciatura en Tecnología Digital</a></li>
            <li><a href="#">Volver al Inicio</a></li>


            


          </ul>
        </div>
        <div class="footer-col">
          <h4>Bibliografía</h4>
          <ul>
            <li><a target="_blank" href="https://www.ibm.com/es-es/topics/quantum-computing">Computación Cuántica - IBM</a></li>
            <li><a target="_blank" href="https://azure.microsoft.com/es-es/resources/cloud-computing-dictionary/what-is-quantum-computing">Computación Cuántica - Microsoft</a></li>
            <li><a target="_blank" href="https://blogthinkbig.com/que-son-qubits-y-tipos">¿Qué son los Qubits?</a></li>
            <li><a target="_blank" href="https://www.jsr.org/hs/index.php/path/article/download/2236/975/14010">Comparación entre Qubits</a></li>
            <li><a target="_blank" href="https://quantumpedia.uk/a-brief-history-of-quantum-computing-e0bbd05893d0#:~:text=The%20Theoretical%20Foundations%20of%20Quantum,Quantum%20Computers%20(2000%E2%80%932021)">Historia de la computación Cuántica</a></li>
            <li><a target="_blank" href="https://www.researchgate.net/publication/336341290_Trends_in_Quantum_Computing">Tendencias en la Computación Cuántica</a></li>
            <li><a target="_blank" href="https://arxiv.org/pdf/2311.10375">Computación Cuántica en el Machine Learning</a></li>
          </ul>
        </div>

        <div class="footer-col">
          <h4>Contacto</h4>
          <div class="social-links">
            <a href="https://github.com/valenvv/vd-tp-final"><i class="fab fa-github"></i></a>
          </div>
          <ul>
            <li><a target="_blank" href="https://www.linkedin.com/in/caterina-villegas-6a623623b/">Caterina Villegas</a></li>
            <li><a target="_blank" href="https://www.linkedin.com/in/valentina-vitetta/">Valentina Vitetta</a></li>
          </ul>
        </div>
      </div>
    </div>
 </footer>
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
  .section { 
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
    margin-bottom: 160px;
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
    font-size: 35px;
    font-weight: normal;
    text-align: center;
    justify-content: center;
    position: relative;
    margin: 0;
    z-index: 1;
  }

  .sub_principioNombres{
    font-weight: lighter;
    font-size: 20px;
    text-align: center;
    justify-content: center;
    position: relative;
    margin-top: 0;
    margin-bottom: 50px;
    z-index: 1;
  }

  .sub_principioPlay{
    font-size:5;
    text-align: center;
    justify-content: center;
    position: relative;
    margin: 0;
    z-index: 1;
    color: #dcc2f8;
  }


  .play{
    z-index: 1;
    cursor: pointer;
    border: none;
    background: none;
    padding: 0;
    max-width: 40px;

  }
  .play:focus {
    outline: none; /* Elimina el contorno al enfocar */
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
      width: 70px;
      margin: 0 auto;
      border-radius: 50px;
  }

  .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: left;
    padding-bottom: 1em;
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
  max-width: 50%;
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
    position: relative;
  }
  .circle-top1{
    margin-top: 3%;
    width: 100%;
    height: 100%; /* Altura de la parte superior circular */
    background-image: linear-gradient(to bottom, #3d3d3d60,rgba(61, 70, 242, 0.02)); /* Degradado interno */
    border-radius: 0% 80% 0 0% / 100% 30% 0 0;
   position: absolute;
    top: 0;
    left: 0;
    z-index: 0; /* Detrás del contenido */
    
  }

  .qubits .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 900px;
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
    color:#e6d2fc;
    font-weight: 750;
    font-size: 30px;
    font-family: 'Arp';
  }

  /* Estilos para el scroller barras*/
  .foreground_container {
    pointer-events: none;
    padding-left: 50%;
    margin-bottom: 10%;
  }
  .step_foreground {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    color: white;
    font-weight: 200;
    padding: 1em;
    margin: 0 0 2em 4em;
  }

  .step_foreground h3{
    font-family: "Arp";
    font-size: 20px;
  }

  .epi_foreground {
    padding: 20px;
    max-width: 300px;
    background-color:rgba(44, 44, 44, 0.5);
    border-radius: 10px;
  }
  .image_container {
    display: flex;
    justify-content: left;
    align-items: left;
    margin-left: 10%;
    height: 100vh;
    transform: translate(0%, -8%);
  }

 
  /* Estilos para el scroller App */
  .graficoApp {
  position: relative;
  width: 80%;
}

.bullets {
    list-style-type: disc; /* Asegura que todas las listas usen puntos como viñetas */
    padding-left: 20px;    /* Asegura que haya suficiente espacio para las viñetas */
}
  .foreground_containerApp {
    pointer-events: none;
    padding-left: 50%;
    overflow-x: hidden;
    max-width: 100%;
    width: 60%;
   
  }
  .image_containerApp{
    /* background-color: #3D46F2; */
    max-width: 100%;
    display: flex;
    align-items: center; 
    width: 82%;
    margin-left: 150px;
    height: 100vh;
    transform: translate(-25%, -8%);
  }
  .step_foregroundApp {
    /* background-color: #3D46F2; */
    display: flex;
    justify-content: end;
    align-items: center;
    height: 100vh;
    width: 80vh;
    max-width: 100%;
    color: white;
    padding: 1em;
    margin: 0 8em 2em 0;
    transform: translateX(18%);
  }
  .epi_foregroundApp {
    padding: 20px;
    height: 50%;
    width: 100%;
    background-color: rgba(30, 30, 30, 0.5);
    /* border: 1px solid #CB9BFF; */
    border-radius: 10px;
    font-weight: 200;
    text-align: left; 
  }
  .titulosApp{
    font-size: 20px; /*PREGUNTAR */
    font-family: 'Arp';
  }

  .modeloActual{
    color:#CB9BFF;
    font-weight: 300;
  }
   
  /* Estilos para la sección de historia */
  .historia {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 60vh;
    text-align: center;
    margin-top: 0;
    margin-bottom: 0%;
    position: relative; /* Para posicionar el degradado interno */
    overflow: hidden; /* Para ocultar el degradado que sobresalga */
    transform: translateY(5.8%);
  }

  .historia .contenido {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 900px;
    z-index: 1; /* Asegura que el contenido esté sobre el degradado */
    position: relative; /* Para asegurar el z-index funcione */

  }

  .historia h2 {
    font-size: 56px;
    margin: 0;
  }

  .historia h3 {
    font-size: 26px;
    margin: 0;

  }
  .circle-top {
    width: 100%;
    height: 100%; /* Altura de la parte superior circular */
    background-color: #3d46f20c;
    background-image: linear-gradient(to bottom, #3d46f210,rgb(7, 8, 27)); /* Degradado interno */
    border-radius: 30% 30% 0 0 / 80% 80% 0 0;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 0; /* Detrás del contenido */
    
  }

  /*Estilos del timeline*/
  .timeline {
    background-image: linear-gradient(to bottom, rgb(7, 8, 27),rgba(7, 9, 52, 0.02)); /* Degradado interno */
        position: relative;
        max-width: 100%;
        margin-top: 0%;
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
   
    @media screen and (max-width: 600px) {
        .timeline::after {
            left: 31px;
        }
    }

  /*Estilos para la sección de desafios*/

  .aplicacion {
    background: linear-gradient(to bottom, #0A122D 5%, #000000 18%); /* Degradado más corto *  margin-top: 200px; /*Adapt fondo*/
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
  max-width: 900px;
  font-weight: 200;
  }

  .aplicacion h2 {
    font-size: 46px;
    margin-bottom: 10px;
    color: #ffffff;
  }

  .parrafosAppIntro {
  font-size: 18px;
  line-height: 1.6;
  margin-bottom: 0;
  }

  .imagen-fondo {
    
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    z-index: 0;
    
  }
  .imagen-fondo img {
  width: 100%;
  height: auto;
  object-fit: cover;
  
}

  /*Estilos para la sección de desafios*/
  
    .desafios {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: auto;
      text-align: center;
      margin: 100px 0 0 0;
      width: 100%;
    }

    .imagen-fondo1 {
    
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    z-index: 0;
    
  }
  .imagen-fondo1 img {
  width: 100%;
  height: auto;
  object-fit: cover;
  
}

    .desafios .contenido {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      max-width: 900px;
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
 


  main{
    /* background-image: url("images/fondofin (4).svg");  */
    background-size: 100vw;
    margin: 0 0;
    z-index: 2;
  }


  /*Estilos para los desafíos*/
  .lista-desafios {
    display: flex;
    flex-direction: column;
    gap: 20px;
    justify-content: flex-start;
    margin-top: 2%;
    margin-bottom: 90px;

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
    font-size: 1.2em;
    font-family: 'Arp';
   

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
    margin-top: 100px;
    
  }
  .mapaSection .contenido {
    max-width: 900px;
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
    align-items: left;
  }
  .step_foregroundm {
    /* background-color: #d0a3ff; */
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    color: white;
    padding: 1em;
    margin: 0 0 10em 0;
  }
  .epi_foregroundm {
    padding: 20px;
    width: 30%;
    background-color: rgba(0, 0, 0, 0.877);
    border-radius: 10px;
  }
  .titulosDesafios{
    font-family: 'Arp';
    font-size: 14px;
  }
/* Estilo conclusion */
.bg-animation {
  justify-content: center;
  align-items: center;
  height: 50vh;
  padding-bottom: 10%;
  text-align: center;
  position: relative; /* Agregar posición relativa para alinear elementos absolutos */
}

.bg-animation .contenido {
  position: absolute; /* Posición absoluta para centrar */
  top: 50%; /* Alineación vertical al centro */
  left: 50%; /* Alineación horizontal al centro */
  transform: translate(-50%, -50%); /* Ajuste para centrar exactamente */
  font-weight: 200;
  max-width: 900px; 
  width: 90%; 
}

.bg-animation h2 {
  font-size: 42px;
  margin-bottom: 10px;
  color: #ff7195;
  font-family: "Arp";
}

.bg-animation p {
  line-height: 1.6;
  margin-bottom: 0;
}

  /* Estilos Footer */
  .container{
    max-width: 1170px;
    margin:auto;
  }
  .row{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  ul{
    list-style: none;
  }
  .footer{
    background-color: #2b2b2d8c;
      padding: 70px 0;
  }
  .footer-col{
    width: 30%;
    padding: 0 15px;
  }
  .footer-col h4{
    font-size: 18px;
    color: #d7b6ff;
    text-transform: capitalize;
    margin-bottom: 35px;
    font-weight: 500;
    position: relative;
    font-family: "Arp";
  }
  .footer-col h4::before{
    content: '';
    position: absolute;
    left:0;
    bottom: -10px;
    background-color: #4a00a5;
    height: 3px;
    box-sizing: border-box;
    width: 50px;
  }
  .footer-col ul li:not(:last-child){
    margin-bottom: 10px;
  }
  .footer-col ul li a{
    font-size: 16px;
    text-transform: capitalize;
    color: #ffffff;
    text-decoration: none;
    font-weight: 300;
    color: #bbbbbb;
    display: block;
    transition: all 0.3s ease;
  }
  .footer-col ul li a:hover{
    color: #ffffff;
    padding-left: 8px;
  }
  .footer-col .social-links a{
    display: inline-block;
    height: 40px;
    width: 40px;
    background-color: rgba(255,255,255,0.2);
    margin:0 10px 10px 0;
    text-align: center;
    line-height: 40px;
    border-radius: 50%;
    color: #ffffff;
    transition: all 0.5s ease;
  }
  .footer-col .social-links a:hover{
    color: #24262b;
    background-color: #ffffff;
  }

  /*responsive*/
  @media(max-width: 767px){
    .footer-col{
      width: 50%;
      margin-bottom: 30px;
  }
  }
  @media(max-width: 574px){
    .footer-col{
      width: 100%;
  }
  }
  
</style>
  

