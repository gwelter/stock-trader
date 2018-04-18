<template>
  <div class="col-sm-6 col-md-4">
    <div class="card">
      <div class="card-header">
        <h3 class="card-title text-success">
          {{stock.name}}
          <small>(Price: {{stock.price}})</small>
        </h3>
      </div>
      <div class="card-body">
        <div>
          <input type="number" class="form-control" v-model="quantity" min="0">
          <button
            class="btn btn-success btn-block"
            @click="buyStock"
            :disabled="quantity <= 0">Buy</button>
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
  methods: {
    buyStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      console.log(order)
      this.quantity = 0
    }
  }
}
</script>

