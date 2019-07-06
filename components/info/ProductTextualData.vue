<template>
  <b-jumbotron :header="title" :lead="pO.description">
    <ProductAvailability :onSale="onSale" :inventory="inventory" :premium="premium" />

    <!-- Details -->
    <b-card>
      <b-row>
        <h2>Details
          <b-button :class="showCollapse ? 'collapsed' : null" :aria-expanded="showCollapse ? 'true' : 'false'" aria-controls="collapse-1" variant="light" @click="showCollapse = !showCollapse">
            <FontAwesomeIcon :icon="['fas', showCollapse ? 'chevron-up' : 'chevron-down']" />
          </b-button>
        </h2>
      </b-row>
      <b-row>
        <b-collapse id="collapse-1" v-model="showCollapse" class="mt-2">
          <b-card>
            <b-list-group>
              <b-list-group-item v-for="(detail, i) in pO.details" :key="i">{{ detail }}</b-list-group-item>
            </b-list-group>
          </b-card>
        </b-collapse>
      </b-row>
    </b-card>

    <!-- Variants -->
    <b-card>
      <b-row>
        <h2>Colors</h2>
      </b-row>
      <b-row>
        <b-list-group horizontal="md">
          <b-list-group-item v-for="(variant, i) in variants" :key="i" class="color-box" :style="{ backgroundColor: variant.color }" @mouseover="$emit('chooseVariant', i)" />
        </b-list-group>
      </b-row>
    </b-card>

    <b-card>
      <b-row>
        <h2>Size</h2>
      </b-row>
      <b-row>
        <b-dropdown id="sizeChoice" :text="chosenSize" class="m-md-2" variant="primary">
          <b-dropdown-item v-for="(size, i) in pO.sizes" :key="i" @click="chooseSize(size)">{{ size }}</b-dropdown-item>
        </b-dropdown>
      </b-row>
    </b-card>

    <b-card>
      <b-row>
        <b-col>
          <b-button variant="primary" :disabled="inventory === 0" @click="addToCart">Add to cart</b-button>
        </b-col>
        <b-col>
          {{ variants[chosenVariant].cart }}
        </b-col>
        <b-col>
          <b-button variant="primary" :disabled="variants[chosenVariant].cart === 0" @click="removeFromCart">Remove from cart</b-button>
        </b-col>
      </b-row>
    </b-card>
  </b-jumbotron>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faChevronDown, faChevronUp } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

import ProductAvailability from '~/components/info/ProductAvailability'

library.add(faChevronDown, faChevronUp)

export default {
  components: {
    FontAwesomeIcon,
    ProductAvailability
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
    // Add a local cart property to each variant
    var variants = this.pO.variants
    for(var i = 0; i < variants.length; i++) {
      variants[i].cart = 0
    }

    return {
      chosenSize: 'Medium',
      variants: variants,
      showCollapse: false
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
    addToCart() {
      this.variants[this.chosenVariant].cart++
      this.variants[this.chosenVariant].inventory--
      this.$emit('addToCart', this.pO.baseId.toString() + this.chosenVariant.toString())
    },
    removeFromCart() {
      this.variants[this.chosenVariant].cart--
      this.variants[this.chosenVariant].inventory++
      this.$emit('removeFromCart', this.pO.baseId.toString() + this.chosenVariant.toString())
    },
    chooseSize(size) {
      this.chosenSize = size
    }
  }
}
</script>
