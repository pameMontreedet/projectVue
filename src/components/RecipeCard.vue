<template>
    <div>
       <div class="card" style="width: 18rem;">
  <img class="card-img-top" :src="recipe.image" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">{{ recipe.title}}</h5>
    <p class="card-text">{{ recipe.description }}</p>
    <button class="btn btn-danger" @click="sendDelete">Delete</button>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
    </div>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      require: true
    }
  },
  methods: {
    sendDelete () {
      this.$emit('recipeDelete', this.recipe.id)
    }
  }
}
</script>

<style scoped>
</style>
