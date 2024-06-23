<script> 
  import Scroller from "@sveltejs/svelte-scroller";
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
    0: "entrelazamiento1.png",
    1: "entrelazamiento2.png",
    2: "entrelazamiento3.png",
    3: "entrelazamiento4.png",
  };
  let showImage = true;
  $: showImage = progress2 < 0.15;
</script>

<main>
  <section class="entrelazamiento-section"  >
    
    
    <!-- Segundo scroller -->
    <Scroller
      top={0}
      threshold={0.8}
      bottom={0.3}
      bind:count={count2}
      bind:index={index2}
      bind:offset={offset2}
      bind:progress={progress2}
    >
      <div slot="background" class="image_container">
        {#if showImage}
        <img src="/images/{charts[index2]}" alt="chart {index2}" class="charts"
        />
        {/if}
      </div>
      <div slot="foreground" class="foreground_container">
        <div class="contenido">
          <h2>Entrelazamiento</h2>
          <p>
            El entrelazamiento cuántico es un fenómeno en el que dos qubits (o dos o más partículas cuánticas cualesquiera) se entrelazan de tal forma que el estado de una partícula no puede describirse independientemente del estado de la otra, sin importar la distancia que las separe.      
          </p>
        </div>
      </div>
    </Scroller>
  
  
  </section>
</main>
<style>
  /* Estilos para el scroller */

  .image_container {
    position: relative;
    padding-bottom: 56.25%; /* Proporción 16:9 (para mantener la relación de aspecto) */
    overflow: hidden;
    width: 50%; /* Ajusta el ancho del contenedor según tus necesidades */
    margin: auto; /* Centra el contenedor horizontalmente */
    transform: translate(50%, 0%);
  }

  .image_container img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: auto;
  }

  .foreground_container {
    pointer-events: none;
    
  }

  .step_foreground {
    display: flex;
    justify-content: end;
    align-items: center;
    height: 0vh;
    
  
    padding: 1em;
    margin: 0 0 2em 0;
  }
  

  .image_container {
    display: flex;
    justify-content: center;
    align-items: center;
  
  }
   /* Estilos para la sección de Entrelazamiento */
   .entrelazamiento-section {
    position: relative;
    padding: 50px 20px;
    /* Ajusta el padding según sea necesario */
  }

  .entrelazamiento-section .contenido {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    position: relative;
    margin-bottom: 20px;
  }

  .entrelazamiento-section h2 {
    font-size: 36px;
    position: relative;
    margin-bottom: 10px;
  }

  .entrelazamiento-section p {
    font-size: 18px;
    position: relative;
    line-height: 1.6;
    margin-bottom: 20px;
  }

  /* Estilos para la sección de Entrelazamiento */
  .entrelazamiento-section {
    
    padding: 50px 20px;
    position: relative;
  }

  .entrelazamiento-section .contenido {
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
    position: relative; /* Puede ser eliminado si no se necesita */
  }

  .entrelazamiento-section h2 {
    font-size: 36px;
    margin-bottom: 10px;
    transform: translate(3%, -190%);
  }

  .entrelazamiento-section p {
    font-size: 18px;
    background-color: black;
    line-height: 1.6;
    margin-bottom: 20px;
    transform: translate( -100%, 10%);
  }
</style>