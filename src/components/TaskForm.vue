<template> 
  <form @submit.prevent="submitForm"> 
    <input v-model="title" placeholder="Заголовок" required /> 
    <input v-model="description" placeholder="Описание" required /> 
    <button type="submit">Добавить задачу</button> 
  </form> 
</template> 
 
<script> 
import { ref } from 'vue'; 
 
export default { 
  setup(_, { emit }) { 
    const title = ref(''); 
    const description = ref(''); 
 
    const submitForm = () => { 
      emit('addTask', { title: title.value, description: description.value }); 
      title.value = ''; 
      description.value = ''; 
    }; 
 
    return { title, description, submitForm }; 
  } 
}; 
</script>