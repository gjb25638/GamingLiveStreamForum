<template>
  <div class="f-link">
    <a v-if="external" target="_blank" :href="link">
      <slot></slot>
    </a>
    <nuxt-link v-else :to="link">
      <slot></slot>
    </nuxt-link>
  </div>
</template>
<script>
export default {
  props: {
    link: {
      type: String,
      default: "#"
    },
    external: {
      type: Boolean,
      default: false
    }
  }
};
</script>
<style scoped>
a {
  text-decoration: none;
  color: inherit;
  height: 100%;
}
</style>
