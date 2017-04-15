
<script>
  import { Dialog } from 'quasar'
  import { setDone } from '../../persistence'
  export default {
    computed: {
      list () {
        return this.$store.state.Expenses.list
      }
    },
    methods: {
      askRemove (expense) {
        const self = this
        Dialog.create({
          title: 'Tem certeza',
          buttons: [
            {
              label: 'Cancelar'
            },
            {
              label: 'Confirmar',
              handler () {
                self.remove(expense)
              }
            }
          ]
        })
      },
      remove (expense) {
        this.$store.commit('REMOVE_EXPENSE', expense)
      },
      toggle (expense) {
        expense.done = !expense.done
        setDone(expense)
      }
    }
  }
</script>

<template>
    <div>
      <div class="expense" v-for="expense in list" @click="toggle(expense)">
        <p :class="{ done: expense.done }">{{ expense.date }} - R$ {{ expense.amount }}</p>
        <p :class="{ done: expense.done }">{{ expense.description }}</p>
        <a href="#" @click.prevent="askRemove(expense)" class="removeLink">remover</a>
      </div>
    </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
    color: #ccc;
  }
  .expense {
    border-bottom: #999 1px solid;
    padding-top: 10px;
    position: relative;
    cursor: pointer;
  }
  .removeLink {
    color: #c00000;
    position: absolute;
    bottom: 10px;
    right: 0;
    font-size: 0.8em;
  }
</style>
