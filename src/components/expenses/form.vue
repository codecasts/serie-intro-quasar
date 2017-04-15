
<script>
    import moment from 'moment'
    import { Utils } from 'quasar'
    export default {
      data () {
        return {
          expense: {
            id: '',
            amount: '',
            description: '',
            date: moment().format('DD/MM/YYYY'),
            done: false
          }
        }
      },
      methods: {
        submit () {
          const cloned = JSON.parse(JSON.stringify(this.expense))
          cloned.id = Utils.uid()
          this.$store.commit('ADD_EXPENSE', cloned)
          this.reset()
        },
        reset () {
          this.expense.amount = ''
          this.expense.description = ''
          this.expense.date = moment().format('DD/MM/YYYY')
          this.$refs.amount.focus()
        }
      }
    }
</script>

<template>
    <form @submit.prevent="submit">
      <input ref="amount" class="my-input" type="number" v-model="expense.amount" placeholder="R$">
      <input class="my-input" type="text" v-model="expense.description" placeholder="Descrição">
      <input class="my-input" type="text" v-model="expense.date" placeholder="Data">
      <button class="primary my-button">Salvar</button>
    </form>
</template>

<style scoped>
  .my-input {
    width: 100%;
    margin-bottom: 20px;
  }
  .my-button {
    width: 100%;
  }
</style>
