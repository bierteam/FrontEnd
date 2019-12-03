<template>
  <div class="about">
    <input id="txtName" @keyup="filterData" v-model="txtInput" type="text" />
    <h1>{{msg}}</h1>
      <div class="items" v-for='item in filterCocktails' :key='item.first_name'>
        <div>{{item.strDrink}} {{item.idDrink}}</div>
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
