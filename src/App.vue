<template>
  <div id="app">
    <!-- <img src="./assets/logo.png">
    <button class="btn btn-success">Button</button>
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <HeaderComponent></HeaderComponent> -->

    <div class="container">
      <div class="row">
        <div class="col">
          <div v-if="isNewRecipe" >
            <RecipeForm @formSaved="recipeFormSave"></RecipeForm>
          </div>
          <button class="btn btn-success float-right" 
          @click="isNewRecipe = !isNewRecipe">
          Create Recipe
          </button>
        </div>
      </div>
      <!-- <RecipeCard v-for="recipe in recipes" 
            :key="recipe.id" 
            :recipe="recipe"
            @cardDelete="deleteCard">
      </RecipeCard> -->


      <div class="row pt-4">
          <div class="col">
              <input type="text" class="form-control" v-model="searchTitle">
          </div>
      </div>

      <div class="row  pt-4">
          <div class="col-sm-12 col-md-4"
          v-for="recipe in filterList" 
          :key="recipe.id">
            <RecipeCard
              :recipe="recipe"
              @cardDelete="deleteCard">
            </RecipeCard>     
          </div>
      </div>
      
    </div>
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
  data(){
    return{
      isNewRecipe: false,
      recipes:[],
      searchTitle:''
    }
  },
  computed: {
    filterList () {
      return this.recipes.filter((recipe) => {
        return recipe.title.toLowerCase().indexOf(this.searchTitle.toLowerCase()) > -1
      })
    }
  },
  mounted () {
    if( localStorage.getItem('recipes') ){
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
      console.log(this.recipes)
    }
  },
  watch:{
    recipes: {
      handler () {
        console.log('Recipe change')
        localStorage.setItem('recipes', JSON.stringify(this.recipes))
      },
      deep: true
    }
  },
  methods: {
    recipeFormSave (recipe) {
      this.recipes.push(recipe)
    },
    deleteCard (id) {
      const index = this.recipes.findIndex((value) => value.id === id)
      console.log('deleteCard id=',id)
      console.log('deleteCard index=',index)
      this.recipes.splice(index, 1);

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
  margin-top: 60px;
}
</style>
