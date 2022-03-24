/* eslint-disable */
<template>
  <div>
    <HeaderVue :totalIncome="state.totalIncome" />
    <FormVue :state="state" @add-income="AddIncome" />
    <IncomeList :state="state" />
  </div>
  
</template>

<script>
import { reactive, computed } from 'vue'
import HeaderVue from './components/HeaderVue.vue'
import FormVue from './components/FormVue.vue'
import IncomeList from './components/IncomeList.vue'

export default {
    name: "App",
    setup() {
        const state = reactive({
            income: [],
            totalIncome: computed(() => {
                let temp = 0;
                if (state.income.length > 0) {
                  for (let i = 0; i < state.income.length; i++) {
                      temp += state.income[i].value;
                  }
                  
                } 
                return temp;
                
            }),
            sortedIncome: computed(() => {
              let temp = [];

              temp = state.income.sort((a, b) => {
                return b.date - a.date;
              })

              return temp;
            })
        });

        function AddIncome (data) {
          let d = data.date.split("-");
          let newD = new Date(d[0], d[1], d[2]);

          state.income = [...state.income, {
            id: Date.now(),
            desc: data.desc,
            value: parseInt(data.value),
            date: newD.getTime()
          }];
          console.log(state.income)
        }

        return {
            HeaderVue,
            state,
            FormVue,
            AddIncome,
            IncomeList
        };
    },
    components: { HeaderVue, FormVue, IncomeList }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background: #EEE;

}
</style>
