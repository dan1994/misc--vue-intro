<template>
  <b-jumbotron :header="title" :lead="pO.description">
    <ProductAvailability
      :onSale="onSale"
      :inventory="inventory"
      :premium="premium"
    />

    <ProductDetails
      :details="pO.details"
    />

    <ProductVariants
      :variants="variants"
      :sizes="pO.sizes"
      @chooseVariant="chooseVariant"
    />

    <ProductToCart
      :cart="variants[chosenVariant].cart"
      :inventory="inventory"
      @addToCart="addToCart"
      @removeFromCart="removeFromCart"
    />
  </b-jumbotron>
</template>

<script>
import ProductAvailability from '~/components/info/ProductAvailability'
import ProductDetails from '~/components/info/ProductDetails'
import ProductVariants from '~/components/info/ProductVariants'
import ProductToCart from '~/components/info/ProductToCart'

export default {
  components: {
    ProductAvailability,
    ProductDetails,
    ProductVariants,
    ProductToCart
  },

  props: {
    pO: {
      type: Object,
      default: () => {}
    },
    premium: {
      type: Boolean,
      default: false
    },
    chosenVariant: {
      type: Number,
      default: 0
    }
  },

  data() {
    var variants = this.pO.variants
    for(var i = 0; i < variants.length; i++) {
      variants[i].cart = 0
    }

    return {
      variants: variants
    }
  },

  computed: {
    title() {
      return this.pO.brand + ' ' + this.pO.product
    },
    inventory() {
      return this.variants[this.chosenVariant].inventory
    },
    onSale() {
      return this.pO.brand === 'Dan\'s'
    }
  },

  methods: {
    chooseVariant(id) {
      this.$emit('chooseVariant', id)
    },
    addToCart() {
      this.variants[this.chosenVariant].cart++
      this.variants[this.chosenVariant].inventory--
      this.$emit('addToCart', this.pO.baseId.toString() + this.chosenVariant.toString())
    },
    removeFromCart() {
      this.variants[this.chosenVariant].cart--
      this.variants[this.chosenVariant].inventory++
      this.$emit('removeFromCart', this.pO.baseId.toString() + this.chosenVariant.toString())
    }
  }
}
</script>
