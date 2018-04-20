<template>
  <div>
    <div class="card">
      <div class="card-header">
        <h3 class="card-title text-info">
          {{stock.name}}
          <small>(Price: {{stock.price | currency}} | Quantity {{stock.quantity}})</small>
        </h3>
      </div>
      <div class="card-body">
        <div>
          <input type="number" class="form-control" v-model="quantity" min="0" :class="{danger: insuficientQuantity}">
          <button
            class="btn btn-info btn-block"
            @click="sellStock"
            :disabled="insuficientQuantity || quantity <= 0">
            {{ insuficientQuantity ? 'Not enough stocks' : 'Sell' }}
            </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    insuficientQuantity () {
      return parseInt(this.quantity) > this.stock.quantity
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock'
    }),
    sellStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.placeSellOrder(order)
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
