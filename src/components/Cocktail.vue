<template>
  <div class="about">
    <input id="txtName" @keyup="filterData" v-model="txtInput" type="text" />
    <h1>{{msg}}</h1>
      <div class="cocktails" v-for='cocktail in filterCocktails' :key='cocktail'>
        <ul>
          <div>{{cocktail.strDrink}}({{cocktail.idDrink}})</div>
          <div class="cocktails" v-for='(ingredient, index) in cocktail.ingredients' :key='index'>
            <li>{{ingredient}}</li>
          </div>
        </ul>
      </div>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data () {
    return {
      txtInput: '',
      filteredCocktails: [],
      cocktails: []
    }
  },
  methods: {
    filterData () {
      if (this.txtInput) {
        this.filteredCocktails = this.filteredCocktails.filter(cocktail => cocktail.strDrink.toLowerCase().includes(this.txtInput.toLowerCase()))
      }
    }
  },
  computed: {
    filterCocktails: function () {
      const data = this.cocktails.filter(cocktail => cocktail.strDrink.toLowerCase().includes(this.txtInput.toLowerCase()))
      return data
    }
  },
  created () {
    axios
      .get('http://localhost:3000/cocktail')
      .then(response => (this.cocktails = response.data))
  }
}
</script>
