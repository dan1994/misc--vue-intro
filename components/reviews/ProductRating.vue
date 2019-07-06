<template>
  <div>
    <FontAwesomeIcon
      v-for="i in [0, 1, 2, 3, 4]"
      :key="i"
      :icon="[solid[i], 'star']"
      @mouseover="ratingPreview = i + 1"
      @mouseleave="ratingPreview = rating"
      @click="$emit('setRating', i + 1)"
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

  props: {
    'rating': {
      type: Number,
      default: 0
    }
  },

  data() {
    return {
      ratingPreview: 0,
      lastRating: 0
    }
  },

  computed: {
    solid() {
      var solidArr = []
      for(var i in [0, 1, 2, 3, 4]) {
        solidArr[i] = i < this.ratingPreview ? 'fas' : 'far'
      }
      return solidArr
    }
  },

  watch: {
    rating(r) {
      this.ratingPreview = r
    }
  }
}
</script>
