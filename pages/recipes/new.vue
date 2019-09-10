<template>
  <form @submit.prevent="submitRecipe">
    <div class="field">
      <label class="label">Recipe Title</label>
      <input
        v-model.trim="title"
        class="input"
        :class="{ 'is-danger': $v.title.$error }"
        type="text"
        @input="$v.title.$touch()"
      />
      <p v-if="!$v.title.minLength && $v.title.$dirty" class="help is-danger">
        Title must be at lease 4 characters.
      </p>
    </div>
    <div class="field">
      <label class="label">Recipe Image URL</label>
      <input
        v-model.trim="image"
        class="input"
        :class="{ 'is-danger': $v.image.$error }"
        type="text"
        @input="$v.image.$touch()"
      />
      <p v-if="!$v.image.required && $v.image.$dirty" class="help is-danger">
        Image URL is required
      </p>
    </div>
    <div class="field">
      <label class="label">Steps</label>
      <textarea
        v-model="steps"
        class="textarea"
        rows="5"
        :class="{ 'is-danger': $v.steps.$error }"
        type="text"
        @input="$v.steps.$touch()"
      >
      </textarea>
      <p v-if="!$v.steps.required && $v.steps.$dirty" class="help is-danger">
        Recipe steps are required.
      </p>
      <p v-if="!$v.steps.minLength && $v.steps.$dirty" class="help is-danger">
        Steps must be at lease 30 characters.
      </p>
    </div>
    <div class="field">
      <label class="label">Category</label>
      <div class="control">
        <div class="select">
          <select v-model="categoryId">
            <option value="1">Dessert</option>
            <option value="2">Healthy Eating</option>
          </select>
        </div>
      </div>
    </div>
    <button :disabled="$v.$invalid" class="button is- primary">Add</button>
  </form>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators'

export default {
  data() {
    return {
      title: '',
      image: '',
      steps: '',
      categoryId: 1
    }
  },
  validations: {
    title: {
      required,
      minLength: minLength(4)
    },
    image: { required },
    steps: {
      required,
      minLength: minLength(30)
    }
  },
  methods: {
    submitRecipe() {
      const recipe = {
        title: this.title,
        image: this.image,
        steps: this.steps,
        categoryId: Number(this.categoryId)
      }
      this.$axios.$post('http://localhost:3001/recipes', recipe)
    }
  }
}
</script>

<style></style>
