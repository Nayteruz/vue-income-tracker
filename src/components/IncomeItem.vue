<template>
  <div class="income-item">
    <div class="remove-item" @click="remove(income)">x</div>
    <div class="desc">{{ income.desc }}</div>
    <div class="price">{{ income.value }} $</div>
    <div class="date">{{ dateFormat() }}</div>
  </div>
</template>

<script>
export default {
  name: "IncomeItem",
  props: {
    income: {
      type: Object,
      default: {}
    }
  },
  setup(props, {emit}){
    const remove = (data) => {
      emit('remove-income', data)
    }

    const dateFormat = () => {
      let d = new Date(props.income.date);
      return `${pad(d.getDate())}-${pad(d.getMonth())}-${d.getFullYear()}`
    }

    function pad(n){
      return n<10 ? '0'+n:n;
    }

    return {
      remove,
      dateFormat
    }
  }
}
</script>

<style scoped>
  .income-item {
    position: relative;
    display: flex;
    padding: 15px 15px 15px 0;
    background: #fff;
    border-radius: 8px;
    max-width: 600px;
    margin: 0 auto 30px;
  }
  .remove-item {
    color: #ef2d2d;
    font-weight: 600;
    font-size: 20px;
    line-height: 1;
    text-align: center;
    margin: 0 15px;
    cursor: pointer;
  }
  .desc {
    color: #666;
    flex: 1 1 100%;
    font-size: 20px;
  }
  .price {
    color: #666;
    min-width: 100px;
    font-size: 20px;
  }
  .date {
    color: #666;
    text-align: right;
    font-size: 20px;
    white-space: nowrap;
  }
</style>