<template>
  <form @submit.prevent="sendForm">
    <input v-model="formData.desc" type="text" placeholder="описание...">
    <input v-model="formData.value" type="number" placeholder="число">
    <input v-model="formData.date" type="date" placeholder="Дата">
    <button type="submit">Отправить</button>
  </form>
</template>

<script>
import { reactive } from "vue";

export default {
  name: "Form",
  props: {
    state: {
      type: Object,
      default: {}
    }
  },
  setup(props, {emit}) {
    const formData = reactive({
      desc: null,
      value: null,
      date: null
    })

    const sendForm = () => {
      emit('add-income', {
        desc:formData.desc,
        value:formData.value,
        date:formData.date
      })
      formData.desc = null;
      formData.value = null;
      formData.date = null;

    }

    return {formData, sendForm}
  }
}
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

form input {
  color: #333;
  border: none;
  outline: none;
  font-size: 20px;
  display: block;
  padding: 5px 15px;
  min-height: 45px;
}

form input::placeholder {
  color: #aaa;
}

form button {
  display: block;
  background: none;
  border: none;
  outline: none;
  color: #fff;
  font-weight: 500;
  text-shadow: 0 1px 3px rgba(0, 0, 0, .2);
  padding: 5px 15px;
  background: #ffce00;
  cursor: pointer;
  font-size: 20px;
}

form input:first-of-type {
  border-radius: 8px 0 0 8px;
}

form button {
  border-radius: 0 8px 8px 0;
}
</style>