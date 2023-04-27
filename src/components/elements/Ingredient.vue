<template>
<span @click="$emit('toggle-selected', name)" :class="selected ? 'inline-flex items-baseline border-2 border-green-600 ml-1' : 'inline-flex items-baseline border-2 ml-1'">
    <img class="self-center w-10 h-10 rounded-full" :src="'http://www.thecocktaildb.com/images/ingredients/' + name + '-Small.png'" :alt=name>
    <span class="text-xl font-semibold mr-2 capitalize">{{name}}</span>
</span>
</template>

<script>

export default {
  name: 'ingredient',
  props: {
    name: {
        type: String, 
        default: "gin",
    },
    selected: Boolean,
  },
}
</script>