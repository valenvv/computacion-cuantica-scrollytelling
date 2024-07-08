<script>
    import { onMount } from 'svelte';
    import AOS from 'aos';
    
    export let name;
    export let date;
    export let left;
    export let eventID;
    export let description;
    export let author;
  
    onMount(() => {
      AOS.init();
    });
  </script>
  
  <svelte:head>
    <link rel="stylesheet" href="https://unpkg.com/aos@next/dist/aos.css" />
  </svelte:head>
  
  <div class="container" class:left={left} class:right={!left} id={eventID} data-aos={left ? 'fade-left' : 'fade-right'}>
    <div class="content">
      <h2>{date}</h2>
      <h2>{name}</h2>
      <p>{description}</p>
    </div>
  </div>
  
  <style>
    /* Estilos para el contenedor de cada evento */
    .container {
      position: relative;
      max-width: 500px; /* Ajusta el ancho máximo según sea necesario */
      margin: 20px auto; /* Centra horizontalmente y agrega margen */
      padding: 20px;
      background-color: #262857;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
  
    /* Estilos condicionales para la posición del evento en la línea de tiempo */
    .left {
      margin-left: 30px; /* Ajusta el margen izquierdo según sea necesario */
    }
  
    .right {
      margin-right: 30px; /* Ajusta el margen derecho según sea necesario */
    }
  
    /* Media queries para responsividad */
    @media screen and (max-width: 600px) {
      .container {
        max-width: 100%; /* Ancho completo en pantallas pequeñas */
        margin: 20px 0; /* Margen superior e inferior */
        padding: 15px; /* Menor espacio de relleno */
      }
  
      .left,
      .right {
        margin-left: 0; /* Reset de margen izquierdo para el lado izquierdo */
        margin-right: 0; /* Reset de margen derecho para el lado derecho */
      }
    }
  
    /* Elementos de diseño para la línea de tiempo */
    .container::after {
      content: '';
      position: absolute;
      width: 50px;
      height: 50px;
      background-color: rgb(255, 255, 255);
      border-radius: 50%;
      top: 50%;
      position: center;
      /* background-color: #5BADD5; las bolitas de shor y google deberian ser de este color */
      background-color: #ffffff;
      text-align: justify;
      z-index: 10;
    }
  
    .left::after {
      left: 530px;
      transform: translate(25%, -50%);
    
    }
    
    .right::after {
      right: 530px;
      transform: translate(-35%, -50%);
    }
  </style>
  