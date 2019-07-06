<template>
  <div>
    <b-card-img :src="img" :alt="product" />
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: String,
      default: ''
    },
    img: {
      type: String,
      default: ''
    }
  }
}
</script>
