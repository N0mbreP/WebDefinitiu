<script setup>
import { ref, computed } from 'vue';

// Definimos las tareas reactivas
const tasks = ref([
  { id: 1, text: 'Tasca 1', completed: false },
  { id: 2, text: 'Tasca 2', completed: true },
  { id: 3, text: 'Tasca 3', completed: false },
  { id: 4, text: 'Tasca 4', completed: true },
  { id: 5, text: 'Tasca 5', completed: false },
]);

// Para el nuevo texto de la tarea
const newTaskText = ref('');

// Para el filtro de mostrar solo pendientes
const showPendingOnly = ref(false);

// Computed property para filtrar las tareas
const filteredTasks = computed(() => {
  if (showPendingOnly.value) {
    return tasks.value.filter(task => !task.completed);
  }
  return tasks.value;
});

// Computed property para contar el total de tareas
const totalTasks = computed(() => tasks.value.length);

// Computed property para contar las tareas pendientes
const pendingTasks = computed(() => tasks.value.filter(task => !task.completed).length);

// Función para añadir una nueva tarea
const addTask = () => {
  if (newTaskText.value.trim() === '') {
    return;
  }
  const newId = tasks.value.length > 0 ? Math.max(...tasks.value.map(task => task.id)) + 1 : 1;
  tasks.value.push({
    id: newId,
    text: newTaskText.value,
    completed: false,
  });
  newTaskText.value = ''; // Limpiar el input
};

// Función para alternar el estado de completado de una tarea
const toggleTaskStatus = (id) => {
  const task = tasks.value.find(task => task.id === id);
  if (task) {
    task.completed = !task.completed;
  }
};

// Función para eliminar una tarea
const deleteTask = (id) => {
  tasks.value = tasks.value.filter(task => task.id !== id);
};
</script>

<template>
  <div class="task-manager">
    <h1>Gestor de Tasques</h1>

    <div class="input-section">
      <input
        type="text"
        v-model="newTaskText"
        @keyup.enter="addTask"
        placeholder="Escriu una nova tasca"
      />
      <button @click="addTask">Afegir</button>
    </div>

    <div class="filter-section">
      <input type="checkbox" id="show-pending" v-model="showPendingOnly" />
      <label for="show-pending">Mostra només pendents</label>
    </div>

    <ul class="task-list">
      <li v-for="task in filteredTasks" :key="task.id" :class="{ completed: task.completed }">
        <span class="task-text">{{ task.text }}</span>
        <button
          @click="toggleTaskStatus(task.id)"
          :class="{ 'btn-mark': !task.completed, 'btn-unmark': task.completed }"
        >
          {{ task.completed ? 'Desmarcar' : 'Completar' }}
        </button>
        <button @click="deleteTask(task.id)" class="btn-delete">🗑️</button>
      </li>
    </ul>

    <div class="summary">
      Total: {{ totalTasks }} | Pendents: {{ pendingTasks }}
    </div>
  </div>
</template>

<style scoped>
.task-manager {
  font-family: Arial, sans-serif;
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #eee;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  font-size: 2em;
}

.input-section {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.input-section input[type="text"] {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1em;
}

.input-section button {
  padding: 10px 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1em;
}

.input-section button:hover {
  background-color: #45a049;
}

.filter-section {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 5px;
}

.filter-section input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.filter-section label {
  font-size: 1em;
  cursor: pointer;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 0;
  border-bottom: 1px dashed #eee;
}

.task-list li:last-child {
  border-bottom: none;
}

.task-list li.completed .task-text {
  text-decoration: line-through;
  color: #888;
}

.task-text {
  flex-grow: 1;
  font-size: 1.1em;
}

.task-list button {
  padding: 8px 12px;
  margin-left: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
  white-space: nowrap; /* Evita que el texto del botón se rompa */
}

.btn-mark {
  background-color: #008CBA; /* Azul */
  color: white;
}

.btn-mark:hover {
  background-color: #007bb5;
}

.btn-unmark {
  background-color: #f44336; /* Rojo */
  color: white;
}

.btn-unmark:hover {
  background-color: #da190b;
}

.btn-delete {
  background-color: #f44336; /* Rojo */
  color: white;
  padding: 8px 10px; /* Un poco más pequeño para el icono */
}

.btn-delete:hover {
  background-color: #da190b;
}

.summary {
  text-align: center;
  margin-top: 20px;
  font-size: 1.1em;
  font-weight: bold;
}
</style>