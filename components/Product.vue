<template>
  <div>
    <b-container fluid>
      <b-row>
        <b-col sm="4">
          <b-card-img :src="img" :alt="pO.product" />
        </b-col>

        <b-col sm="8">
          <b-jumbotron :header="title" :lead="pO.description">
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

            <!-- Details -->
            <b-card>
              <b-row>
                <h2>Details<b-button v-b-toggle.collapse-1 variant="light">|</b-button></h2>
              </b-row>
              <b-row>
                <b-collapse id="collapse-1" class="mt-2">
                  <b-card>
                    <b-list-group>
                      <b-list-group-item v-for="detail in pO.details" :key="detail.id">{{ detail.content }}</b-list-group-item>
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
                  <b-list-group-item v-for="variant in variants" :key="variant.id" class="color-box" :style="{ backgroundColor: variant.color }" @mouseover="chooseVariant(variant.id)" />
                </b-list-group>
              </b-row>
            </b-card>

            <b-card>
              <b-row>
                <h2>Size</h2>
              </b-row>
              <b-row>
                <b-dropdown id="sizeChoice" :text="chosenSize" class="m-md-2" variant="primary">
                  <b-dropdown-item v-for="size in pO.sizes" :key="size.id" @click="chooseSize(size.size)">{{ size.size }}</b-dropdown-item>
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
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
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
    // Add a local cart property to each variant
    var variants = this.pO.variants
    for(var i = 0; i < variants.length; i++) {
      variants[i].cart = 0
    }

    return {
      'chosenVariant': 0,
      'chosenSize': 'Medium',
      'variants': variants
    }
  },

  computed: {
    img() {
      return this.variants[this.chosenVariant].img
    },
    title() {
      return this.pO.brand + ' ' + this.pO.product
    },
    inventory() {
      return this.variants[this.chosenVariant].inventory
    },
    onSale() {
      return this.pO.brand === "Dan's"
    },
    shipping() {
      if(this.premium) {
        return 'Free'
      }
      return '2.99$'
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
    chooseVariant(id) {
      this.chosenVariant = id
    },
    chooseSize(size) {
      this.chosenSize = size
    }
  }
}
</script>

<style>
.outOfStock {
  text-decoration: line-through;
}
</style>
