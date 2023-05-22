<template>
  <div class="col mb-4">
    <div class="card card-success">
      <div class="card">
        <h5 class="card-header">
          {{ stock.name }}<small> (Price: {{ stock.price }})</small>
        </h5>
      </div>
      <div class="card-body d-flex justify-content-between gap-3">
        <div>
          <input
            type="number"
            class="form-control"
            placeholder="Quantity"
            v-model="quantity"
            :class="{ danger: insufficientFunds }"
          />
        </div>
        <div class="text-end">
          <button
            class="btn btn-success"
            @click="buyStock"
            :disabled="quantity <= 0 || insufficientFunds"
          >
            {{ insufficientFunds ? "Insufficient Funds" : "Buy" }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.danger {
  border: 1px solid red;
}
</style>
<script>
export default {
  props: ["stock"],
  data() {
    return { quantity: 0 }
  },
  computed: {
    funds() {
      return this.$store.getters.funds
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds
    },
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      }
      this.$store.dispatch("buyStock", order)
      this.quantity = 0
    },
  },
}
</script>
