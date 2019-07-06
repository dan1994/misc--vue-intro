<template>
  <div>
    <b-row>
      <b-badge v-show="onSale" variant="primary">On Sale!</b-badge>
    </b-row>
    <b-row>
      Shipping: {{ shipping }}
    </b-row>
    <b-row>
      <p v-if="inventory > 5">{{ inventory }} In stock</p>
      <p v-else-if="inventory > 0">Only {{ inventory }} left</p>
      <p v-else :class="{ outOfStock: (inventory === 0) }">Out of stock</p>
    </b-row>
  </div>
</template>

<script>
export default {
  props: {
    onSale: {
      type: Boolean,
      default: false
    },
    inventory: {
      type: Number,
      default: 0
    },
    premium: {
      type: Boolean,
      default: false
    }
  },

  computed: {
    shipping() {
      if(this.premium) {
        return 'Free'
      }
      return '2.99$'
    }
  }
}
</script>

<style scoped>
.outOfStock {
  text-decoration: line-through;
}
</style>
