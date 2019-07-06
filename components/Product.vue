<template>
  <div>
    <ProductInfo :pO="pO" :premium="premium" @addToCart="addToCart" @removeFromCart="removeFromCart" />
    <ProductReviewsArea />
  </div>
</template>

<script>
import ProductInfo from '~/components/info/ProductInfo'
import ProductReviewsArea from '~/components/reviews/ProductReviewsArea'

export default {
  components: {
    ProductInfo,
    ProductReviewsArea
  },

  props: {
    pO: {
      type: Object,
      default: () => {}
    },
    premium: {
      type: Boolean,
      default: false
    }
  },

  methods: {
    addToCart(id) {
      this.$emit('addToCart', id)
    },
    removeFromCart(id) {
      this.$emit('removeFromCart', id)
    }
  }
}
</script>
