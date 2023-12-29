<template>
  <div class="todo-container">
  <h1>Lista de Tareas</h1>
  <div>
    <input type="text" v-model='inputValue'>
    <button @click="handleClick()">Agregar Tarea</button>
  </div>

  <div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">{{ task }}
      <button @click="deleteTask(index)">Eliminar</button>
      <button @click="updateTask(index)">Editar</button></li>
    </ul>
  </div>
</div>
</template>


<script lang="ts" setup>
  import {Ref,ref} from 'vue';

    let tasks:Ref<Array<string>> = ref([])
    let inputValue:Ref<string | null> = ref(null)

    const handleClick = () => {
      if (inputValue.value) {
        tasks.value.push(inputValue.value)
        inputValue.value = null
      } else alert('No has introducido ninguna tarea')
      
    }
    const deleteTask = (index: number) => {
      tasks.value.splice(index,1)
    }
    const updateTask = (index:number) => {
      if(!inputValue.value) return
      tasks.value[index] = inputValue.value
    }

</script>


<style scoped>
.todo-container{
  width: 100vw;
  height: 100wh;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
}

.task-item{
  text-decoration: none;
}
</style>