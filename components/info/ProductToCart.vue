<template>
  <div>
    <b-card>
      <b-row>
        <b-col>
          <b-button variant="primary" :disabled="inventory === 0" @click="$emit('addToCart')">Add to cart</b-button>
        </b-col>
        <b-col>
          {{ cart }}
        </b-col>
        <b-col>
          <b-button variant="primary" :disabled="cart === 0" @click="$emit('removeFromCart')">Remove from cart</b-button>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<script>
export default {
  props: {
    cart: {
      type: Number,
      default: 0
    },
    inventory: {
      type: Number,
      default: 0
    }
  }
}
</script>
