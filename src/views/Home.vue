<template>
  <div class="home">
    <div class="grid grid-cols-6 gap-4">
    <Ingredient @toggle-selected="toggleSelected" :name="ingredient.name" :selected="ingredient.selected" v-for="ingredient in ingredients"/>
    </div>
    <!-- <p>{{ selected_ingredients }}</p> -->
    <!-- <p>{{ cocktails }}</p> -->
    <br>
    <h2 v-show="selected_ingredients.length>0 & cocktails.length===0" class="text-gray-500 text-2xl font-semibold">No cocktail found</h2>
    <div class="grid grid-cols-3 gap-4">
    <Cocktail :id="cocktail.idDrink" v-for="cocktail in cocktails"/>
    </div>
    <br>
  </div>
</template>

<script>
// imports
import axios from "axios"
import Cocktail from '../components/elements/Cocktail'
import Ingredient from '../components/elements/Ingredient'
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
    Cocktail,
    Ingredient
  }, 
  data() {
    return {
      ingredients: [],
      cocktails: [],
    }
  }, 
  computed: {
    selected_ingredients() {
      var sel = this.ingredients.filter(ingr => ingr.selected).map(ingr => ingr.name).join(",")
      sel = sel.split(' ').join('_')
      return sel
    }
  },
  watch: {
    selected_ingredients: function() {
      this.getCocktails()
    }
  },
  methods: {
    toggleSelected(name) {
      this.ingredients = this.ingredients.map(ingr => ingr.name===name ? {...ingr, selected: !ingr.selected} : ingr)
    },
    async getCocktails() {
      if (!this.selected_ingredients) {
        console.log("empty!")
        this.cocktails = []
      } else {
        axios.get('https://www.thecocktaildb.com/api/json/v2/9973533/filter.php?i='+this.selected_ingredients)
        .then(res => {
          const drinks = res.data.drinks
          if (typeof drinks === 'string') {
            this.cocktails = []
          } else {
            drinks.forEach(drink => drink.idDrink=Number(drink.idDrink))
            this.cocktails = drinks
          }
        })
      }
    },
  },
  created() {
    this.ingredients = [
       {name: "vodka",
       selected: false},
       {name: "gin",
       selected: false},
       {name: "rum",
       selected: false},
       {name: "tequila",
       selected: false},
       {name: "amaretto",
       selected: false},
       {name: "baileys irish cream",
       selected: false},
       {name: "lemon peel",
       selected: false},
       {name: "lime",
       selected: false},
       {name: "orange",
       selected: false},
       {name: "banana",
       selected: false},
       {name: "cherry",
       selected: false},
       {name: "mango",
       selected: false},
       {name: "tonic water",
       selected: false},
       {name: "coca-cola",
       selected: false},
       {name: "milk",
       selected: false},
       {name: "coffee",
       selected: false},
       {name: "lemon juice",
       selected: false},
       {name: "orange juice",
       selected: false}
    ]
  },
}
</script>
