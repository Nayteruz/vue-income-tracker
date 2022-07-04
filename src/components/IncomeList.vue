<template>
  <div class="income-list">
    <IncomeItem :income="data" v-for="data in state.sortedIncome" :key="data.id"  @remove-income="remove"/>
  </div>
</template>

<script>
import IncomeItem from "./IncomeItem.vue";
export default {
  name: "IncomeList",
  components: {IncomeItem},
  props: {
    state: {
      type: Object,
    }
  },
  setup(props, {emit}){

    const remove = (data) => {
      emit('remove-income', data)
    }

    return {
      remove
    }
  }

}
</script>

<style scoped>
  .income-list {
    margin-top: 30px;
    padding: 15px;
  }
</style>