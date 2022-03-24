<template>
  <div class="income-list">
      <IncomeItem v-for="data in state.sortedIncome" :key="data.id" :income="data" />
  </div>
</template>

<script>
import IncomeItem from './IncomeItem.vue'

export default {
    props: {
        state: Object
    },
    setup () {
        return {
            IncomeItem
        }
    },
    components: {
        IncomeItem
    }
}
</script>

<style scope>
.income-list {
    margin-top: 30px;
    padding: 15px;
}
</style>