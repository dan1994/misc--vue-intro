<template>
  <div>
    <b-container fluid>
      <b-row>
        <!-- Products -->
        <b-col sm="11">
          <Product :pO="productObj" :premium="true" @addToCart="addToCart" @removeFromCart="removeFromCart" />
        </b-col>
        <!-- Cart -->
        <b-col sm="1">
          <b-row>
            <b-card>Cart <b-badge pill variant="primary">{{ cart.length }}</b-badge></b-card>
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
      'cart': [],
      'productObj': {
        'baseId': 1443,
        'brand': 'Dan\'s',
        'product': 'Socks',
        'description': 'The best shoes ever',
        'details': [
          'High quality',
          'Great for winters!'
        ],
        'variants': [
          {
            'color': 'green',
            'img': 'https://cdn.shopify.com/s/files/1/0920/4808/products/1-green_800x.jpg?v=1536352096',
            'inventory': 6
          },
          {
            'color': 'blue',
            'img': 'https://cdn.shopify.com/s/files/1/1278/9255/products/SM-VANNUCCI-V1126RB.jpg?v=1484940185',
            'inventory': 0
          },
          {
            'color': 'red',
            'img': 'https://images-na.ssl-images-amazon.com/images/I/71BVuXCWmfL._UL1500_.jpg',
            'inventory': 2
          }
        ],
        'sizes': [
          'Small',
          'Medium',
          'Large'
        ]
      }
    }
  },

  methods: {
    addToCart(id) {
      this.cart.push(id)
    },
    removeFromCart(id) {
      this.cart.pop(id)
    }
  }
}
</script>

<style>
.container {
  margin: auto;
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
