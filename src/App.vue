<template>
  <div class="arriba">
    <h1>Random Gif Cat</h1>
    <div class="formulario">
      <div class="contenedor-formulario">
        <div class="row">
          <label>Titulo:</label>
          <input v-model="formulario.titulo" type="text" />
        </div>
        <div class="row">
          <label>Filtro:</label>
          <select v-model="formulario.filtro">
            <option v-for="filtro in filtros" :key="filtro" :value="filtro">
              {{ filtro }}
            </option>
          </select>
        </div>
        <div class="row">
          <label>Color:</label>
          <select v-model="formulario.color">
            <option
              v-for="(color, index) in colores"
              :key="index"
              :value="color.valor"
            >
              {{ color.nombre }}
            </option>
          </select>
          <div :style="muestraColor" class="cajita-color"></div>
        </div>
        <div class="row">
          <label>Tamaño:</label>
          <input
            @keydown="soloNumeros"
            v-model="formulario.tamano"
            type="number"
          />
        </div>
      </div>
    </div>
    <div class="abajo">
      <button @click="crearGato">Obtener mi gatito</button>
      <img :src="urlGato" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      colores: [
        { valor: "red", nombre: "Rojo" },
        { valor: "pink", nombre: "Rosa" },
        { valor: "green", nombre: "Verde" },
        { valor: "blue", nombre: "Azul" },
        { valor: "yellow", nombre: "Amarillo" },
        { valor: "black", nombre: "Negro" },
      ],
      filtros: ["blur", "mono", "sepia", "negative", "paint", "pixel"],

      formulario: {
        titulo: null,
        filtro: "blur",
        color: "red",
        tamano: null,
      },

      urlGato: "",
    };
  },

  computed: {
    muestraColor() {
      return `background-color: ${this.formulario.color}`;
    },
  },

  methods: {
    soloNumeros(e) {
      if (e.key === "Backspace") {
        return;
      }

      if (!/[0-9]/.test(e.key)) {
        return e.preventDefault();
      }
    },
    crearGato() {
      this.urlGato = `https://cataas.com/cat/gif/says/${this.formulario.titulo}?filter=${this.formulario.filtro}&color=${this.formulario.color}&size=${this.formulario.tamano}`;
    },
  },
};
</script>

<style>
:root {
  --text-color: #2c3e50;
  --first-color: lightblue;
  --second-color: lightcoral;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  color: var(--text-color);
}
h1 {
  text-align: center;
  padding-top: 4rem;
  padding-bottom: 4rem;
}
.arriba {
  width: 100%;
  min-height: 100vh;
  background-color: var(--first-color);
}

.formulario {
  width: 100%;
  padding: 1rem;
  background-color: var(--second-color);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.row {
  padding: 2vh;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
}
.abajo {
  padding: 5vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
button {
  text-align: center;
  padding: 10px;
  margin-bottom: 20px;
}
section {
  width: 100%;
}
.cajita-color {
  width: 20px;
  height: 20px;
  background-color: red;
  border-radius: 50%;
  margin-left: 30px;
}

label{
  font-size: 1rem;
  margin-right: 30px;
  text-align: left;
}
</style>