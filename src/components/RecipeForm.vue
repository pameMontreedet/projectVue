<template>
  <div>
<form @submit.prevent="save">
  <div class="form-group">
    <label for="">Title</label>
    <input type="text" class="form-control" id="title" placeholder="Example input" v-model="recipe.title">
  </div>
  <div class="form-group">
    <label for="">Description</label>
    <input type="text" class="form-control" id="description" placeholder="Another input" v-model="recipe.description">
  </div>
   <div class="form-group">
    <label for="">Image</label>
    <input type="text" class="form-control" id="image" placeholder="Another input"  v-model="recipe.image">
  </div>
  {{recipe}}
  <button class="btn btn-danger">Cancel</button>
  <button type="submit" class="btn btn-primary">Save</button>
</form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      recipe: {
        title: '',
        description: '',
        image: ''
      }
    }
  },
  methods: {
    save () {
      this.$emit('formSaved', this.recipe)
    }
  }
}
</script>

<style scoped>

</style>
