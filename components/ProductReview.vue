<template>
  <div>
    <b-jumbotron lead="Write a Review">
      <b-form v-if="show" @submit="onSubmit" @reset="onReset">
        <b-form-group id="input-group-1" label="Title" label-for="review_title" description="Give your review an indicative title">
          <b-form-input id="review_title" v-model="review.title" required placeholder="Title" />
        </b-form-group>

        <b-form-group id="input-group-2" label="Your Review" label-for="review_text">
          <b-form-textarea id="review_text" v-model="review.text" placeholder="In my opinion..." rows="3" max-rows="6" />
        </b-form-group>

        <ProductRating />

        <b-button type="submit" variant="success">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
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
        text: ''
      },
      show: true
    }
  },

  methods: {
    onSubmit(evt) {
      evt.preventDefault()
      alert(JSON.stringify(this.form))
    },

    onReset(evt) {
      evt.preventDefault()
      // Reset our form values
      this.review.title = ''
      this.review.text = ''
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  }
}
</script>
