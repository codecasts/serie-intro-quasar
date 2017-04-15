
<script>
  import CcForm from './expenses/form.vue'
  import CcList from './expenses/list.vue'
  import { getExpenses } from '../persistence'
  export default {
    components: { CcForm, CcList },
    mounted () {
      this.$store.commit('SET_EXPENSES', getExpenses())
    },
    computed: {
      list () {
        return this.$store.state.Expenses.list
      }
    }
  }
</script>

<template>
  <q-layout>
    <div slot="header" class="toolbar">
      <q-toolbar-title :padding="0">
        Despesas em Dinheiro Vivo
      </q-toolbar-title>
    </div>
    <div class="container">
      <cc-form></cc-form>
      <hr v-show="list.length > 0">
      <cc-list></cc-list>
    </div>
  </q-layout>
</template>

<style scoped>
  .container {
    padding: 20px;
  }
</style>
