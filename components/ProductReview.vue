<template>
  <div>
    <b-jumbotron lead="Write a Review">
      <b-form @submit.prevent="onSubmit">
        <b-form-group id="input-group-1" label="Title" label-for="review_title" description="Give your review an indicative title">
          <b-form-input id="review_title" v-model="review.title" required placeholder="Title" />
        </b-form-group>

        <b-form-group id="input-group-2" label="Your Review" label-for="review_text">
          <b-form-textarea id="review_text" v-model="review.text" placeholder="In my opinion..." rows="3" max-rows="6" />
        </b-form-group>

        <ProductRating :resetRating="resetRating" @setRating="setRating" />

        <b-button type="submit" variant="success">Submit</b-button>
      </b-form>
    </b-jumbotron>
  </div>
</template>

<script>
import ProductRating from '~/components/ProductRating'

export default {
  components: {
    ProductRating
  },

  data() {
    return {
      review: {
        title: '',
        text: '',
        rating: 0
      },
      resetRating: false
    }
  },

  methods: {
    setRating(rating) {
      this.resetRating = false
      this.review.rating = rating
    },
    onSubmit() {
      this.$emit('submitReview', JSON.parse(JSON.stringify(this.review)))
      this.review.title = ''
      this.review.text = ''
      this.resetRating = true
    }
  }
}
</script>
