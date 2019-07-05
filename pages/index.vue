<template>
  <div>
    <div class="nav-bar" />

    <b-container fluid class="product">
      <b-row>
        <b-col class="product-img" sm="3">
          <b-card-img :src="img" :alt="product" />
        </b-col>

        <b-col class="product-info" sm="8">
          <b-jumbotron :header="title" :lead="description">
            <b-row>
              <b-badge v-show="onSale" variant="primary">On Sale!</b-badge>
            </b-row>
            <b-row>
              <p v-if="inventory > 5">{{ inventory }} In stock</p>
              <p v-else-if="inventory > 0">Only {{ inventory }} left</p>
              <p v-else :class="{ outOfStock: (inventory == 0) }">Out of stock</p>
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
                      <b-list-group-item v-for="detail in details" :key="detail.id">{{ detail.content }}</b-list-group-item>
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
                  <span >
                    <b-dropdown-item v-for="size in sizes" :key="size.id" @click="chooseSize(size.size)">{{ size.size }}</b-dropdown-item>
                  </span>
                </b-dropdown>
              </b-row>
            </b-card>

            <b-card>
              <b-row>
                <b-col>
                  <b-button variant="primary" :disabled="inventory == 0" @click="addToCart">Add to cart</b-button>
                </b-col>
                <b-col>
                  <b-button variant="primary" :disabled="cart == 0" @click="removeFromCart">Remove from cart</b-button>
                </b-col>
              </b-row>
            </b-card>
          </b-jumbotron>
        </b-col>

        <!-- Cart -->
        <b-col sm="1">
          <b-row>
            <b-card>Cart <b-badge pill variant="primary">{{ cart }}</b-badge></b-card>
          </b-row>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      'brand': 'Dan\'s',
      'product': 'Socks',
      'description': 'The best shoes ever',
      'chosenVariant': 0,
      'chosenSize': 'Medium',
      'details': [
        {
          'id': 0,
          'content': 'High quality'
        },
        {
          'id': 1,
          'content': 'Great for winters!'
        }
      ],
      'variants': [
        {
          'id': 0,
          'color': 'green',
          'img': 'https://cdn.shopify.com/s/files/1/0920/4808/products/1-green_800x.jpg?v=1536352096',
          'inventory': 6
        },
        {
          'id': 1,
          'color': 'blue',
          'img': 'https://cdn.shopify.com/s/files/1/1278/9255/products/SM-VANNUCCI-V1126RB.jpg?v=1484940185',
          'inventory': 0
        },
        {
          'id': 2,
          'color': 'red',
          'img': 'https://images-na.ssl-images-amazon.com/images/I/71BVuXCWmfL._UL1500_.jpg',
          'inventory': 2
        }
      ],
      'sizes': [
        {
          'id': 0,
          'size': 'Small'
        },
        {
          'id': 1,
          'size': 'Medium'
        },
        {
          'id': 2,
          'size': 'Large'
        }
      ],
      'cart': 0
    }
  },

  computed: {
    img() {
      return this.variants[this.chosenVariant].img
    },
    title() {
      return this.brand + ' ' + this.product
    },
    inventory() {
      return this.variants[this.chosenVariant].inventory
    },
    onSale() {
      return this.brand === "Dan's"
    }
  },

  methods: {
    addToCart() {
      this.cart++
      this.inventory--
    },
    removeFromCart() {
      this.cart--
      this.inventory++
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
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: left;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.outOfStock {
  text-decoration: line-through;
}
</style>
