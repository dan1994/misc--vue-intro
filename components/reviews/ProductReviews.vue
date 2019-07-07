<template>
  <div>
    <b-jumbotron header="Reviews" lead="Here you can find other customers' reviews">
      <p v-if="reviews.length === 0">No reviews yet</p>
      <b-card v-for="review in reviews" v-else :key="review.length" :title="review.title">
        <p>Rating: {{ review.rating }}</p>
        <p v-if="review.recomended">Recomended by the customer :)</p>
        <p v-else>Not recomended by the customer :(</p>
        <p>{{ review.text }}</p>
      </b-card>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    reviews: {
      type: Array,
      default: () => []
    }
  }
}
</script>
