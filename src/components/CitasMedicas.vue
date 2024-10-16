<!-- 
      Este componente se encarga de mostrar la información de una cita médica en una card
      ":class="gravedad"" aplica una clase adicional a la tarjeta 
      dependiendo del valor de la propiedad "gravedad" (alta, media, baja), 
      lo que permite cambiar el color de fondo según la gravedad de la cita.
    -->

<template>
    <div class="card" :class="gravedad">
      <h3>Paciente</h3>
      <span>{{ paciente }}</span>
      <h3>Fecha</h3>
      <span>{{ fecha }}</span>
      <h3>Hora</h3>
      <span>{{ hora }}</span>
      <h3>Gravedad</h3>
      <span>{{ gravedad }}</span>
      <h3>Motivo</h3>
      <span>{{ motivo }}</span>

       <!-- 
      Botón para eliminar la cita.
      emite un evento llamado "eliminar" al componente padre.
      También pasa el valor de la propiedad "paciente" al componente padre como argumento del evento.
    -->
      <button @click="$emit('eliminar', paciente)">Eliminar Cita</button>
    </div>
  </template>
  
  <script>
  export default {
   // Define las propiedades que el componente espera recibir del componente padre.
    props: ["paciente", "fecha", "hora", "gravedad", "motivo"],
  };
  </script>
  
  <style scoped> /* Estilo para la tarjeta */
  .card {
    border: 1px solid #060606;
    color: black;
    border-radius: 5px;
    padding: 10px;
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 200px;
    height: 70%;
    max-height: 600px;
  }
  .card button {
    margin-top: 10px;
  }
  
  /* Colores según gravedad */
  .alta {
    background-color: red;
    color: white;
  }
  
  .media {
    background-color: yellow;
    color: black;
  }
  
  .baja {
    background-color: green;
    color: black;
  }
  </style>