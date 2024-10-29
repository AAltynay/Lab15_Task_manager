<template> 
  <div :style="{ backgroundColor: isCompleted ? '#d4edda' : '#f8d7da' }" class="task"> 
    <h2>{{ task.title }}</h2> 
    <p>{{ task.description }}</p> 
    <input type="checkbox" v-model="isCompleted" @change="toggleCompleted" /> 
    <button @click="removeTask">Удалить</button> 
    <button @click="showDetails">Подробнее</button> 
    <slot v-if="showDetail">{{ task.description }}</slot> 
  </div> 
</template> 
 
<script> 
export default { 
  props: ['task'], 
  data() { 
    return { 
      showDetail: false, 
      isCompleted: this.task.completed, // Локальная копия состояния completed 
    }; 
  }, 
  watch: { 
    // Следите за изменениями в пропсе и обновляйте локальное состояние 
    task: { 
      handler(newTask) { 
        this.isCompleted = newTask.completed; 
      }, 
      deep: true, 
      immediate: true, 
    }, 
  }, 
  methods: { 
    removeTask() { 
      this.$emit('removeTask', this.task.id); 
    }, 
    toggleCompleted() { 
      this.isCompleted = !this.isCompleted; // Меняем локальную копию 
      this.$emit('toggleCompleted', this.task.id, this.isCompleted); // Отправляем обновленное состояние 
    }, 
    showDetails() { 
      this.showDetail = !this.showDetail; 
    }, 
  }, 
}; 
</script> 
 
<style> 
.task { 
  padding: 10px; 
  margin: 10px 0; 
  border: 1px solid #ccc; 
} 
</style>