<template>
  <Header :totalIncome="state.totalIncome"/>
  <Form @add-income="AddIncome"/>
  <IncomeList :state="state" @remove-income="remove" />
</template>

<script>
import Header from "./src/components/Header.vue";
import Form from "./src/components/Form.vue";
import IncomeList from "./src/components/IncomeList.vue";
import {reactive, computed} from 'vue';

export default {
  components: {
    Header,
    Form,
    IncomeList
  },
  setup() {
    const state = reactive({
      income: [],
      totalIncome: computed(() => {
        return state.income.reduce((prevVal, currentVal) => prevVal + currentVal?.value || 0, 0) ?? 0;
      }),
      sortedIncome: computed(() => {
        return state.income.sort((a, b)=>{
          return b.date - a.date;
        })
      })
    })

    const AddIncome = (data) => {
      let d = data.date.split('-');
      let newD = new Date(d[0], d[1], d[2])

      state.income = [...state.income, {
        id: Date.now(),
        desc: data.desc ?? '',
        value: parseInt(data.value),
        date: newD.getTime()
      }]
    }

    const remove = (data) => {
      state.income = state.income.filter(i => i !== data);
    }

    return {
      state,
      AddIncome,
      remove
    }
  }


}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}

body {
  background: #eee;
  min-height: 100vh;

}

#app {
  min-height: 100%;
}
</style>
