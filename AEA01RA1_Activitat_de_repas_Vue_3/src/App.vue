<template>
  <div class="center-box">
    <h1>Llistat de Tasques</h1>

    <div class="add-task">
      <input v-model="textNova" placeholder="Afegeix una tasca nova" type="text"/>
      <button @click="afegirNova">Afegir</button>
    </div>

    <div class="checkbox-container">
      <input type="checkbox" v-model="veurePendents" id="veurePendents" />
      <label for="veurePendents">Mostra només pendents</label>
    </div>

    <ul style="list-style: none; padding: 0; width: 100%">
      <li v-for="tasca in tasquesVisibles" :key="tasca.id" class="task">
        <span :style="{ textDecoration: tasca.feta ? 'line-through' : 'none' }">{{ tasca.titol }}</span>
        <div class="task-buttons">
          <button class="complete" @click="alternarEstat(tasca)">
            {{ tasca.feta ? "Desmarcar" : "Completar" }}
          </button>
          <button class="delete" @click="borrarTasca(tasca.id)">
            <i class="fas fa-trash"></i>
          </button>
        </div>
      </li>
    </ul>

    <p class="stats">Total: {{ total }} | Pendents: {{ pendents }}</p>
    
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import "@fortawesome/fontawesome-free/css/all.min.css";

const llistaTasques = ref([
  { id: 1, titol: "Tasca 1", feta: true },
  { id: 2, titol: "Tasca 2", feta: false },
  { id: 3, titol: "Tasca 3", feta: false },
  { id: 4, titol: "Tasca 4", feta: false },
]);

const textNova = ref("");

const veurePendents = ref(false);

const afegirNova = () => {
  if (textNova.value.trim() === "") return;

  let nouIdentificador = 1;
  if (llistaTasques.value.length > 0) {
    nouIdentificador = llistaTasques.value[llistaTasques.value.length - 1].id + 1;
  }

  llistaTasques.value.push({
    id: nouIdentificador,
    titol: textNova.value,
    feta: false,
  });

  textNova.value = "";
};

const borrarTasca = (id) => {
  llistaTasques.value = llistaTasques.value.filter((item) => item.id !== id);
};

const alternarEstat = (tasca) => {
  tasca.feta = !tasca.feta;
};

const tasquesVisibles = computed(() => {
  return veurePendents.value ? llistaTasques.value.filter((t) => !t.feta) : llistaTasques.value;
});

const total = computed(() => llistaTasques.value.length);
const pendents = computed( () => llistaTasques.value.filter((t) => !t.feta).length);

</script>

<style scoped>
body,
html {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f0f2f5;
}

.center-box {
  width: 500px;
  padding: 40px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

h1 {
  color: #1a1a1a;
  margin: 0 0 30px 0;
  text-align: center;
  font-size: 28px;
  font-weight: 600;
}

.add-task {
  display: flex;
  width: 100%;
  gap: 10px;
  margin-bottom: 25px;
}

.add-task input[type="text"] {
  flex: 1;
  padding: 14px 16px;
  font-size: 15px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.add-task input[type="text"]:focus {
  outline: none;
  border-color: #2196f3;
}

.add-task button {
  padding: 14px 24px;
  font-size: 15px;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  background-color: #2196f3;
  color: white;
}

.add-task button:hover {
  background-color: #1976d2;
}

.add-task button:active {
  background-color: #1565c0;
}

.checkbox-container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 25px;
  font-size: 15px;
  gap: 8px;
}

.checkbox-container input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.checkbox-container label {
  cursor: pointer;
  color: #555;
  font-weight: 500;
}

.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 18px;
  font-size: 15px;
  background-color: #fafafa;
  border: 1px solid #e8e8e8;
  border-radius: 8px;
  margin-bottom: 10px;
  width: 100%;
  box-sizing: border-box;
}

.task:hover {
  background-color: #f5f5f5;
  border-color: #d0d0d0;
}

.task span {
  flex: 1;
  color: #333;
  font-weight: 500;
}

.task-buttons {
  display: flex;
  gap: 8px;
}

.complete,
.delete {
  font-size: 14px;
  font-weight: 600;
  padding: 8px 14px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  color: white;
}

.complete {
  background-color: #4caf50;
}

.complete:hover {
  background-color: #43a047;
}

.complete:active {
  background-color: #388e3c;
}

.delete {
  background-color: #f44336;
}

.delete:hover {
  background-color: #e53935;
}

.delete:active {
  background-color: #d32f2f;
}

.stats {
  margin-top: 20px;
  font-size: 15px;
  color: #666;
  font-weight: 500;
  text-align: center;
}

</style>