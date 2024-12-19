<template>
  <div class="container">
    <div class="containerSon_Input">
      <div class="input-group">
        <input
          class="form-control"
          placeholder="Agregar una nueva tarea"
          v-model="texto"
        />
        <span class="input-group-btn">
          <img
            src="/img/add.svg"
            @click="Agregar"
            style="width: 2.2em; min-width: auto;"
          />
        </span>
      </div>
    </div>
    <div class="containerSon_List">
      <div class="listHead">
        <span>ToDo list by Iron Bit</span>
        <img
          src="/img/recycle-bin.svg"
          @click="delete_full"
          style="width: 1.5em; min-width: auto;"
        />
      </div>
      <div class="redondear">
        <div v-if="lista.length">
          <div v-for="(todo, index) in lista" :key="todo.id">
            <div class="listBody">
              <span
                class="texto-item"
                @dblclick="editarTarea(todo, index)"
                >{{ todo.nuevoTexto }}</span
              >
              <img
                src="/img/remove.svg"
                @click="delete_one(todo.id)"
                style="width: 1.5em; min-width: auto;"
              />
            </div>
          </div>
        </div>
        <p v-else>{{ textoAux }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textoAux: "No hay ToDo´s, tomate un café !",
      texto: "",
      lista: [],
    };
  },
  mounted() {
    this.cargarDesdeLocalStorage();
  },
  methods: {
    Agregar() {
      if (this.texto.trim() === "") return alert("La tarea no puede estar vacía");

      this.lista.push({
        id: Date.now(),
        nuevoTexto: this.texto.trim(),
      });
      this.texto = "";
      this.guardarEnLocalStorage();
    },
    delete_full() {
      if (confirm("¿Estás seguro de eliminar todas las tareas?")) {
        this.lista = [];
        this.guardarEnLocalStorage();
      }
    },
    delete_one(id) {
      this.lista = this.lista.filter((todo) => todo.id !== id);
      this.guardarEnLocalStorage();
    },
    editarTarea(todo, index) {
      const nuevoTexto = prompt(
        "Edita la tarea:",
        todo.nuevoTexto
      );
      if (nuevoTexto !== null && nuevoTexto.trim() !== "") {
        this.lista[index].nuevoTexto = nuevoTexto.trim();
        this.guardarEnLocalStorage();
      }
    },
    guardarEnLocalStorage() {
      localStorage.setItem("todo-list", JSON.stringify(this.lista));
    },
    cargarDesdeLocalStorage() {
      const datosGuardados = localStorage.getItem("todo-list");
      if (datosGuardados) {
        this.lista = JSON.parse(datosGuardados);
      }
    },
  },
};
</script>

<style>
.container {  
  display: flex;
  flex-direction: column;
  min-height: 70vh;
  /*border: 1px solid #000*/
}
.containerSon_Input{
  margin: 1.5em 0em 1.5em 0em;
}
.input-group-btn{
  background: rgb(255 255 255);
}
.redondear{
  border: 2px solid rgb(255, 255, 255);
  border-radius: 0em 0em 0.5em 0.5em;
}
.listHead{
  border-radius: 0.7em 0.7em 0em 0em;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background: rgb(2, 185, 2);
  padding: 0.5em 0.2em 0.5em 0.5em;
}
.listBody{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background: rgb(255, 255, 255);
  padding: 0.8em 0.2em 1em 0.5em;
}
.texto-item{
  padding: 0em 5em 0em 0em;
}
p{
  text-align: center;
  background: rgb(255, 255, 255);
  padding: 0.8em 1em 1em 1em;
  margin: 0em;
}
</style>

