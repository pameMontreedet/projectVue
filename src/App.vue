<template>
  <div id="app">

    <HeaderComponent></HeaderComponent>
    <div class="container">
      <div class="row">
         <div class="col">
        <button class="btn btn-success float-right"
        @click="isNewRecipe = !isNewRecipe">
          Create Recipe
        </button>
        </div>
      </div>
       <div v-if="isNewRecipe">
        <RecipeForm @formSaved="setRecipelist"></RecipeForm>
      </div>
     <div class="row pt-4">
         <div class="col">
        <input type="text" class="form-control" v-model="searchTitle" />
        </div>
      </div>
      <div class="row pt-4">
         <div class="col md-3" v-for="recipe in filterList" :key="recipe.id">
    <RecipeCard @recipeDelete="deleterecipecard" :recipe="recipe"></RecipeCard>
    </div>
      </div>
    </div>
     <button class="btn btn-success">Click Me</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HeaderComponent from './components/HeaderComponent.vue'
import RecipeCard from './components/RecipeCard.vue'
import RecipeForm from './components/RecipeForm.vue'
export default {
  name: 'app',
  components: {
    HelloWorld,
    HeaderComponent,
    RecipeCard,
    RecipeForm
  },
  data () {
    return {
      isNewRecipe: false,
      searchTitle: '',
      recipes: [
        {
          id: '1',
          title: 'Pizza',
          description: 'xxx xxxx adadfb adafds ajklf asdflasdf dsajk dfasdf',
          image: 'https://images.unsplash.com/photo-1506354666786-959d6d497f1a?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=86c8c1fd5e9e5b384696472a095c42ac&auto=format&fit=crop&w=1500&q=80'
        }, {
          id: '2',
          title: 'Hamberger',
          description: 'xxx xxxx adadfb adafds ajklf asdflasdf dsajk dfasdf',
          image: 'https://images.unsplash.com/photo-1518304256228-bb65fd3df672?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=67f3dae2c86fb8fc1009e5cc823cec19&auto=format&fit=crop&w=800&q=60'
        },
        {
          id: '3',
          title: 'Spaketti',
          description: 'xxx xxxx adadfb adafds ajklf asdflasdf dsajk dfasdf',
          image: 'https://images.unsplash.com/photo-1516100882582-96c3a05fe590?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=bb8f920efd9334f4237e960bedd9dde7&auto=format&fit=crop&w=800&q=60'
        }
      ]
    }
  },
  computed: {
    filterList () {
      return this.recipes.filter(recipe => {
        return recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase()) > -1
      }
      )
    }
  },
  mounted () {
    if (localStorage.getItem('recipes')) {
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
      console.log('mouted: ' + this.recipes)
    }
  },
  watch: {
    recipes: {
      handler () {
        console.log('aaaaaaa')
        localStorage.setItem('recipes', JSON.stringify(this.recipes))
      },
      deep: true
    }
  },
  methods: {
    setRecipelist (recipe) {
      recipe.id = this.recipes.length === 0 ? 1 : (this.recipes[this.recipes.length - 1].id) + 1
      this.recipes.push(recipe)
      this.isNewRecipe = false
    },
    deleterecipecard (id) {
      alert(id)
      const index = this.recipes.findIndex((value) => value.id === id)
      this.recipes.splice(index, 1)
      alert('deleted')
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
