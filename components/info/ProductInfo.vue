<template>
  <div>
    <b-row>
      <b-col sm="4">
        <ProductImg :product="pO.product" :img="img" />
      </b-col>
      <b-col sm="8">
        <ProductTextualData
          :pO="pO"
          :premium="premium"
          :chosenVariant="chosenVariant"
          @chooseVariant="chooseVariant"
          @addToCart="addToCart"
          @removeFromCart="removeFromCart"
        />
      </b-col>
    </b-row>
  </div>
</template>

<script>
import ProductImg from '~/components/info/ProductImg'
import ProductTextualData from '~/components/info/ProductTextualData'

export default {
  components: {
    ProductImg,
    ProductTextualData
  },

  props: {
    'pO': {
      'type': Object,
      'default': {}
    },
    'premium': {
      'type': Boolean,
      'default': false
    }
  },

  data() {
    return {
      'chosenVariant': 0
    }
  },

  computed: {
    img() {
      return this.pO.variants[this.chosenVariant].img
    }
  },

  methods: {
    addToCart(id) {
      this.$emit('addToCart', id)
    },
    removeFromCart(id) {
      this.$emit('removeFromCart', id)
    },
    chooseVariant(id) {
      this.chosenVariant = id
    }
  }
}
</script>
