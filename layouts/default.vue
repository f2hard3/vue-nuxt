<template>
  <div>
    <navigation-bar />
    <section class="section">
      <nuxt />
    </section>
  </div>
</template>

<script>
import NavigationBar from '../components/NavigationBar'

export default {
  components: {
    'navigation-bar': NavigationBar
  }
}
</script>

<style></style>
