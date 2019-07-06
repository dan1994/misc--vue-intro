<template>
  <div>
    <b-jumbotron header="Write a Review" lead="This will help other customers to choose wisely">
      <b-form @submit.prevent="onSubmit">
        <b-form-group id="input-group-1" label="Title" label-for="reviewTitle" description="Give your review an indicative title">
          <b-form-input id="reviewTitle" v-model="review.title" required placeholder="Title" />
        </b-form-group>

        <b-form-group id="input-group-2" label="Your Review" label-for="reviewText">
          <b-form-textarea id="reviewText" v-model="review.text" placeholder="In my opinion..." rows="3" max-rows="6" />
        </b-form-group>

        <b-form-group label="Would you recomend this product?">
          <b-form-radio-group v-model="review.recomended" :options="recomendedOpts" plain stacked required />
        </b-form-group>

        <ProductRating :rating="review.rating" @setRating="setRating" />

        <b-button type="submit" variant="success">Submit</b-button>
      </b-form>
    </b-jumbotron>
  </div>
</template>

<script>
import ProductRating from '~/components/reviews/ProductRating'

export default {
  components: {
    ProductRating
  },

  data() {
    return {
      recomendedOpts: [
        {
          text: 'Sure Would!',
          value: true
        },
        {
          text: 'Not So Much...',
          value: false
        }
      ],
      review: {
        title: '',
        text: '',
        recomended: true,
        rating: 0
      }
    }
  },

  methods: {
    setRating(rating) {
      this.review.rating = rating
    },
    onSubmit() {
      this.$emit('submitReview', JSON.parse(JSON.stringify(this.review)))
      this.review.title = ''
      this.review.text = ''
      this.review.rating = 0
    }
  }
}
</script>
