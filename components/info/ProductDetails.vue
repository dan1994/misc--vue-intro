<template>
  <div>
    <b-card>
      <b-row>
        <h2>Details
          <b-button
            :class="showCollapse ? 'collapsed' : null"
            :aria-expanded="showCollapse ? 'true' : 'false'"
            aria-controls="collapse-1"
            variant="light"
            @click="showCollapse = !showCollapse"
          >
            <FontAwesomeIcon :icon="['fas', showCollapse ? 'chevron-up' : 'chevron-down']" />
          </b-button>
        </h2>
      </b-row>
      <b-row>
        <b-collapse id="collapse-1" v-model="showCollapse" class="mt-2">
          <b-card>
            <b-list-group>
              <b-list-group-item v-for="(detail, i) in details" :key="i">{{ detail }}</b-list-group-item>
            </b-list-group>
          </b-card>
        </b-collapse>
      </b-row>
    </b-card>
  </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faChevronDown, faChevronUp } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faChevronDown, faChevronUp)

export default {
  components: {
    FontAwesomeIcon
  },

  props: {
    details: {
      type: Array,
      default: () => []
    }
  },

  data() {
    return {
      showCollapse: false
    }
  }
}
</script>
