<template>
  <div>
    <app-category
      v-for="category in categories"
      :key="category.id"
      :category="category"
    ></app-category>
  </div>
</template>

<script>
import Category from '../components/Category'

export default {
  components: { 'app-category': Category },
  asyncData({ $axios }) {
    return $axios.get(`http://localhost:3001/categories`).then((res) => ({
      categories: res.data
    }))
  }
}
</script>

<style></style>
