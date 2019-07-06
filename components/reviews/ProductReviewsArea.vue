<template>
  <div>
    <WriteProductReview @submitReview="submitReview" />
    <ProductReviews :reviews="reviews" />
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
      reviews: []
    }
  },

  methods: {
    submitReview(review) {
      this.reviews.push(review)
    }
  }
}
</script>
