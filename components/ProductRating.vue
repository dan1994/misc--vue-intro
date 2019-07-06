<template>
  <div>
    <FontAwesomeIcon
      v-for="i in [0, 1, 2, 3, 4]"
      :key="i - 1"
      :icon="[solid[i], 'star']"
      @mouseover="setRatingPreview(i + 1)"
      @mouseleave="unsetRatingPreview"
      @click="setRating(i + 1)"
    />
  </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faStar as faStarRegular } from '@fortawesome/free-regular-svg-icons'
import { faStar as faStarSolid } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faStarRegular, faStarSolid)

export default {
  components: {
    FontAwesomeIcon
  },

  data() {
    return {
      'rating': 0,
      'ratingPreview': 0
    }
  },

  computed: {
    solid() {
      var solidArr = []
      solidArr[0] = 'far'
      for(var i in [0, 1, 2, 3, 4]) {
        solidArr[i] = i < this.ratingPreview ? 'fas' : 'far'
      }
      return solidArr
    }
  },

  methods: {
    setRatingPreview(rating) {
      this.ratingPreview = rating
    },
    unsetRatingPreview() {
      this.ratingPreview = this.rating
    },
    setRating(rating) {
      this.rating = rating
    }
  }
}
</script>
