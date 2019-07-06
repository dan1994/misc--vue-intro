<template>
  <div>
    <b-nav tabs>
      <b-nav-item v-for="(tab, i) in tabs" :key="i" :active="activeTab === i" @click="activeTab = i">{{ tab }}</b-nav-item>
    </b-nav>
    <WriteProductReview v-if="activeTab === 0" @submitReview="submitReview" />
    <ProductReviews v-else-if="activeTab === 1" :reviews="reviews" />
  </div>
</template>

<script>
import WriteProductReview from '~/components/reviews/WriteProductReview'
import ProductReviews from '~/components/reviews/ProductReviews'

export default {
  components: {
    WriteProductReview,
    ProductReviews
  },

  data() {
    return {
      reviews: [],
      tabs: [
        'Write a Review',
        'Reviews'
      ],
      activeTab: 0
    }
  },

  methods: {
    submitReview(review) {
      this.reviews.push(review)
    }
  }
}
</script>
