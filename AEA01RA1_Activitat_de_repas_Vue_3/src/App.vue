<script setup></script>

<template>
  <div class="center-box">
    <h1>Gestor de Tasques</h1>
    
    <div class="add-task">
      <input type="text" placeholder="Ecriu una nova tasca">
      <button>Afegir</button>
    </div>
    
    <div class="checkbox-container">
      <label>
        <input type="checkbox"> Mostra només pendents
      </label>
    </div>
    
    <div class="task">
      <span>Tasca 1</span>
      <div class="task-buttons">
        <button class="complete">Completar</button>
        <button class="delete">🗑️</button>
      </div>
    </div>
    <div class="task">
      <span>Tasca 2</span>
      <div class="task-buttons">
        <button class="complete">Completar</button>
        <button class="delete">🗑️</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
body, html {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
}

.center-box {
  width: 400px;
  padding: 30px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Título */
h1 {
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

/* Contenedor input + botón */
.add-task {
  display: flex;
  width: 100%;
  gap: 10px;
  margin-bottom: 20px;
}

.add-task input[type="text"] {
  flex: 1;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.add-task button {
  padding: 10px 15px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: #2196F3;
  color: white;
  transition: background 0.3s;
}

.add-task button:hover {
  background-color: #1976D2;
}

/* Checkbox centrado */
.checkbox-container {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.checkbox-container input[type="checkbox"] {
  margin-right: 5px;
}

/* Tareas más grandes */
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 15px 10px;
  font-size: 18px;
  background-color: #f9f9f9;
  border-radius: 5px;
  margin-bottom: 10px;
}

/* Botones de la tarea */
.task-buttons {
  display: flex;
  gap: 5px;
}

.complete {
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 8px 12px;
  cursor: pointer;
}

.complete:hover {
  background-color: #45a049;
}

.delete {
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 8px 12px;
  cursor: pointer;
}

.delete:hover {
  background-color: #da190b;
}
</style>
