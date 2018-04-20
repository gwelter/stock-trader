<template>
  <div class="col-md-4">
    <div class="card">
      <div class="card-header">
        <h3 class="card-title text-success">
          {{stock.name}}
          <small>(Price: {{stock.price | currency}})</small>
        </h3>
      </div>
      <div class="card-body">
        <div>
          <input type="number" class="form-control" v-model="quantity" min="0" :class="{danger: insuficientFunds}">
          <button
            class="btn btn-success btn-block"
            @click="buyStock"
            :disabled="insuficientFunds || quantity <= 0">
            {{ insuficientFunds ? 'Insuficient Funds' : 'Buy'}}
            </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    funds () {
      return this.$store.getters.funds
    },
    insuficientFunds () {
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods: {
    buyStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: parseInt(this.quantity)
      }
      this.$store.dispatch('buyStock', order)
      this.quantity = 0
    }
  }
}
</script>

<style scoped>
  .danger {
    border: 1px solid red;
  }
</style>
