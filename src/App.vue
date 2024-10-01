<template>
  <div id="app">
    <div class="container">
      <h1>Lista de tareas</h1>
      <div class="input-container">
        <input 
          v-model="nuevaTarea" 
          @keyup.enter="agregarTarea" 
          placeholder="Añadir una nueva tarea" 
          class="task-input"
        />
        <button @click="agregarTarea" class="add-button">Añadir</button>
      </div>
      
      <ul class="task-list">
        <li v-for="(tarea, indice) in tareas" :key="indice" class="task-item">
          <span :class="{ completada: tarea.completada }" @click="alternarCompletada(indice)" class="task-text">
            {{ tarea.texto }}
          </span>
          <button @click="eliminarTarea(indice)" class="delete-button">✖</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevaTarea: '',
      tareas: [
        { texto: "Construir una app de Lista de Tareas", completada: false }
      ]
    };
  },
  methods: {
    agregarTarea() {
      if (this.nuevaTarea.trim()) {
        this.tareas.push({ texto: this.nuevaTarea, completada: false });
        this.nuevaTarea = "";
      }
    },
    eliminarTarea(indice) {
      this.tareas.splice(indice, 1);
    },
    alternarCompletada(indice) {
      this.tareas[indice].completada = !this.tareas[indice].completada;
    }
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  background-color: #f4f4f9;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background-color: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
}

h1 {
  text-align: center;
  color: #4a90e2;
  margin-bottom: 1.5rem;
  font-size: 2rem;
}

.input-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.task-input {
  width: 75%;
  padding: 0.75rem;
  font-size: 1rem;
  border-radius: 4px;
  border: 1px solid #ddd;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
}

.add-button {
  width: 20%;
  padding: 0.75rem;
  background-color: #4a90e2;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.add-button:hover {
  background-color: #357ab8;
}

.task-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem;
  background-color: #f9f9f9;
  margin-bottom: 0.5rem;
  border-radius: 4px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease;
}

.task-item:hover {
  background-color: #e3e3e3;
}

.task-text {
  cursor: pointer;
  flex-grow: 1;
  color: #333;
}

.task-text.completada {
  text-decoration: line-through;
  color: #888;
}

.delete-button {
  background-color: transparent;
  border: none;
  color: #e74c3c;
  font-size: 1.25rem;
  cursor: pointer;
  padding-left: 1rem;
  transition: color 0.3s ease;
}

.delete-button:hover {
  color: #c0392b;
}

@media screen and (max-width: 600px) {
  .container {
    padding: 1.5rem;
  }

  h1 {
    font-size: 1.75rem;
  }

  .task-input {
    font-size: 0.9rem;
    padding: 0.6rem;
  }

  .add-button {
    padding: 0.6rem;
  }
}
</style>
