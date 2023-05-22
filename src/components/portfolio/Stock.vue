<template>
  <div class="col mb-4">
    <div class="card card-info">
      <div class="card">
        <h5 class="card-header">
          {{ stock.name
          }}<small>
            (Price: {{ stock.price }} || Quantity: {{ stock.quantity }})</small
          >
        </h5>
      </div>
      <div class="card-body d-flex justify-content-between gap-3">
        <div>
          <input
            type="number"
            class="form-control"
            placeholder="Quantity"
            v-model="quantity"
            :class="{ danger: insufficientQuantity }"
          />
        </div>
        <div class="text-end">
          <button
            class="btn btn-info"
            @click="sellStock"
            :disabled="quantity <= 0 || insufficientQuantity"
          >
            {{ insufficientQuantity ? "Not enough Stocks" : "Sell" }}
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
import { mapActions } from "vuex"

export default {
  props: ["stock"],
  data() {
    return { quantity: 0 }
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity
    },
  },
  methods: {
    ...mapActions({ placeSellOrder: "sellStock" }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      }
      this.placeSellOrder(order)
      this.quantity = 0
    },
  },
}
</script>
