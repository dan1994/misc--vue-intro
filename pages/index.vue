<template>
  <div>
    <div class="nav-bar" />
    <b-container fluid>
      <b-row>
        <b-col sm="11">
          <Product :pO="productObj" :premium="true" />
          <Product :pO="productObj" :premium="false" />
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
import Product from '~/components/Product.vue'

export default {
  components: {
    Product
  },
  data() {
    return {
      'cart': 0,
      'productObj': {
        'brand': 'Dan\'s',
        'product': 'Socks',
        'description': 'The best shoes ever',
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
        ]
      }
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
