<template>
  <div>
    <FontAwesomeIcon
      v-for="i in [0, 1, 2, 3, 4]"
      :key="i"
      :icon="[solid[i], 'star']"
      @mouseover="mouseover = i + 1"
      @mouseleave="mouseover = -1"
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
      mouseover: -1
    }
  },

  computed: {
    solid() {
      var solidArr = []
      for(var i in [0, 1, 2, 3, 4]) {
        solidArr[i] = i < this.ratingPreview ? 'fas' : 'far'
      }
      return solidArr
    },
    ratingPreview() {
      if(this.mouseover !== -1) {
        return this.mouseover
      }
      return this.rating
    }
  }
}
</script>
