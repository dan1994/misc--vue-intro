<template>
  <div>
    <b-card>
      <b-row>
        <h2>Colors</h2>
      </b-row>
      <b-row>
        <b-list-group horizontal="md">
          <b-list-group-item v-for="(variant, i) in variants" :key="i" class="color-box" :style="{ backgroundColor: variant.color }" @mouseover="$emit('chooseVariant', i)" />
        </b-list-group>
      </b-row>
    </b-card>

    <b-card>
      <b-row>
        <h2>Size</h2>
      </b-row>
      <b-row>
        <b-dropdown id="sizeChoice" :text="chosenSize" class="m-md-2" variant="primary">
          <b-dropdown-item v-for="(size, i) in sizes" :key="i" @click="chooseSize(size)">{{ size }}</b-dropdown-item>
        </b-dropdown>
      </b-row>
    </b-card>
  </div>
</template>

<script>
export default {
  props: {
    variants: {
      type: Array,
      default: () => []
    },
    sizes: {
      type: Array,
      default: () => []
    }
  },

  data() {
    return {
      chosenSize: 'Medium'
    }
  },

  methods: {
    chooseSize(size) {
      this.chosenSize = size
    }
  }
}
</script>
