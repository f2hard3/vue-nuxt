<script>
export default {
  validate({ params }) {
    return !isNaN(+params.id)
  },
  asyncData({ $axios, params }) {
    return $axios
      .get(`http://localhost:3001/recipes?categoryId=${params.id}`)
      .then((res) => {
        return { recipes: res.data }
      })
  }
}
</script>

<style></style>
