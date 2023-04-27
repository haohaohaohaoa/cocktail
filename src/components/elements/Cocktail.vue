<template>
<div v-if="cocktail" class="max-w-md mx-auto px-4 bg-white shadow-lg rounded-lg my-20">
<div class="flex justify-center md:justify-end -mt-16">
<div>
    <a target="_blank" :href="'https://www.thecocktaildb.com/drink/'+id" class="block w-24 h-24"><img class="object-cover rounded-full border-2 border-gray-500" :src="cocktail.strDrinkThumb"></a>
</div>
<h3 class="text-gray-800 pt-2 mx-2 text-2xl font-semibold font-serif">
{{ cocktail.strDrink }}
</h3>
<!-- <p>{{ id }} {{ cocktail.idDrink }}</p> -->
<p class="mx-2 text-left font-thin text-gray-800 text-sm text-ellipsis overflow-hidden max-h-20">
    {{ cocktail.strInstructions }}
</p>
</div>
<p class="text-slate-500 text-right mt-2 text-xs">
{{ cocktail.strIngredient1 }}{{ cocktail.strIngredient2 ? `, ${cocktail.strIngredient2}`: "" }}{{ cocktail.strIngredient3 ? `, ${cocktail.strIngredient3}`: "" }}{{ cocktail.strIngredient4 ? `, ${cocktail.strIngredient4}`: "" }}{{ cocktail.strIngredient5 ? `, ${cocktail.strIngredient5}`: "" }}{{ cocktail.strIngredient6 ? `, ${cocktail.strIngredient6}`: "" }}{{ cocktail.strIngredient7 ? `, ${cocktail.strIngredient7}`: "" }}{{ cocktail.strIngredient8 ? `, ${cocktail.strIngredient8}`: "" }}
</p>
</div>
</template>

<script>
import axios from "axios"
export default {
    name: 'Cocktail', 
    data() {
        return {
            cocktail: null,
        }
    },
    props: {
        id: Number
    },
    watch: {
        id: function() {
            this.getCocktail()
        }
    },
    mounted() {
        this.getCocktail()
    },
    methods: {
        async getCocktail() {
            axios.get(`https://www.thecocktaildb.com/api/json/v2/9973533/lookup.php?i=${this.id}`).then(response => this.cocktail = response.data.drinks[0])
        },
    },
}
</script>