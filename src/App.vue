<!-- Formulario para agregar nuevas citas -->
<template>
  <div class="contenedor-principal">
  <h1>Ingresar nueva consulta médica</h1>
  <form @submit.prevent="agregarCard">
    <div class="form-container">
      <div>
        <label :style="{ color: paciente ? 'black' : 'red' }" for="paciente"
          >Paciente</label>
        <input v-model="paciente" type="text" id="paciente"/>
      </div>
      <div>
        <label :style="{ color: fecha ? 'black' : 'red' }" for="fecha"
          >Fecha</label>
        <input v-model="fecha" type="date" id="fecha"/>
      </div>
      <div>
        <label :style="{ color: hora ? 'black' : 'red' }" for="hora"
          >Hora</label>
        <input v-model="hora" type="time" id="hora"/>
      </div>
      <div>
        <label :style="{ color: gravedad ? 'black' : 'red' }" for="gravedad"
          >Gravedad</label>
        <select v-model="gravedad" id="gravedad">
          <option value="">Seleccionar</option>
          <option value="alta">Alta</option>
          <option value="media">Media</option>
          <option value="baja">Baja</option>
        </select>
      </div>
      <div>
        <label :style="{ color: motivo ? 'black' : 'red' }" for="motivo"
          >Motivo</label>
        <input v-model="motivo" type="text" id="motivo"/>
      </div>
    </div>
    <div class="boton-agregar">
      <button type="submit" :disabled="!formularioCompleto">Agregar</button>
    </div>
  </form>

  <section class="cards-container">
    <CitasMedicas
      v-for="(card, i) in cards"
      :key="i"
      :paciente="card.paciente"
      :fecha="card.fecha"
      :hora="card.hora"
      :gravedad="card.gravedad"
      :motivo="card.motivo"
      @eliminar="eliminarCard(card.paciente)"
    />

    <p v-if="cards.length === 0" class="mensaje">
      Aún no hay consultas registradas
    </p>
  </section>
</div>
</template>

<script>
import CitasMedicas from "./components/CitasMedicas.vue";

export default {
  data() {
    return {
      cards: [], // Array para almacenar las citas médicas
      // Campos del formulario
      paciente: "",
      fecha: "",
      hora: "",
      gravedad: "",
      motivo: "",
    };
  },
  components: {
    CitasMedicas,
  },
  //verifica si los campos del formulario están llenos
  computed: {
    formularioCompleto() { 
      return (
        this.paciente && this.fecha && this.hora && this.gravedad && this.motivo
      );
    },
  },
   // Método para agregar una nueva cita médica al array 'cards'
  methods: {
    agregarCard(event) {
      event.preventDefault();
      //si el formulario está completo renderiza la card
      if (this.formularioCompleto) {
        this.cards.push({ //agrega objeto al array de la card
          paciente: this.paciente,
          fecha: this.fecha,
          hora: this.hora,
          gravedad: this.gravedad,
          motivo: this.motivo,
        });
        // Limpiar formulario después de agregar la cita médica
        this.paciente = "";
        this.fecha = "";
        this.hora = "";
        this.gravedad = "";
        this.motivo = "";
      }
    },
    // Método para eliminar una cita médica del array 'cards'
    eliminarCard(paciente) {
      // Filtra el array 'cards' y mantiene las citas cuyo paciente sea diferente al recibido
      this.cards = this.cards.filter((card) => card.paciente !== paciente);
    },
  },
};
</script>



<style scoped>

.contenedor-principal {
  display: flex;
  flex-direction: column;
  align-items: center; /* Centrado horizontal */
  width: 100%; /* El contenedor ocupará todo el ancho disponible */
}
* {
  font-family: "Roboto", sans-serif;
}


body,
html,
#app { /* Es importante aplicar estos estilos al elemento raíz (#app) */
  height: 100%;
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}


h1 {
  text-align: center;
  margin-bottom: 40px; 
}

/* Estilos del formulario */
form {
  width: 100%; 
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f9f9f9;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  font-weight: bold;
  margin-bottom: 30px;
}

/* Estilos para el contenedor de los campos del formulario */
.form-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;
}

/* Estilos para cada grupo de etiqueta e input */
.form-container > div {
  display: flex;
  flex-direction: column;
  width: 100%;
}

/* Estilos para inputs y select */
input,
select {
  width: 100%;
  padding: 5px;
  font-size: 14px;
  box-sizing: border-box;
}

/* Estilos para el botón de agregar */
.boton-agregar {
  margin-top: 15px;
  width: 100%;
  display: flex;
  justify-content: center;
}

button {
  background-color: #91f6a3;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 14px;
  cursor: pointer;
}

button:disabled {
  background-color: #c9c9c9;
  cursor: not-allowed;
}

/* Estilos para el contenedor de las cards */
.cards-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 20px;
  gap: 20px;
  justify-content: center;
  width: 90%;
  max-width: 800px;
}

/* Mensaje cuando no hay consultas */
.mensaje {
  font-weight: bold;
  margin-top: 20px;
  color: red;
  width: 100%;
  text-align: center;
}
</style>