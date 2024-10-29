<template> 
  <div> 
    <h1>Список задач ({{ totalTasks }})</h1> 
    <TaskForm @addTask="addTask" /> 
    <div v-for="task in tasks" :key="task.id"> 
      <Task  
        :task="task"  
        @removeTask="removeTask"  
        @toggleCompleted="toggleCompleted"  
      /> 
    </div> 
    <p>Выполненные задачи: {{ completedTasks }}</p> 
  </div> 
</template> 
 
<script> 
import { ref, computed } from 'vue'; 
import Task from './TaskT01.vue'; 
import TaskForm from './TaskForm.vue'; 
 
export default { 
  components: { Task, TaskForm }, 
  setup() { 
    const tasks = ref([]); 
     
    const totalTasks = computed(() => tasks.value.length); 
    const completedTasks = computed(() => tasks.value.filter(task => task.completed).length); 
 
    const addTask = (newTask) => { 
      tasks.value.push({ ...newTask, id: Date.now(), completed: false }); 
    }; 
 
    const removeTask = (id) => { 
      tasks.value = tasks.value.filter(task => task.id !== id); 
    }; 
 
    const toggleCompleted = (id) => { 
      const task = tasks.value.find(task => task.id === id); 
      if (task) task.completed = !task.completed; 
    }; 
 
    return { tasks, totalTasks, completedTasks, addTask, removeTask, toggleCompleted }; 
  } 
}; 
</script>