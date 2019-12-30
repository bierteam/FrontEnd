<template>
  <div class="about">
    <input id="txtName" @keyup="filterData" v-model="txtInput" type="text" placeholder="Search.." />
    <div class="cocktails">
      <div class="cocktail" v-for="cocktail in filterCocktails" :key="cocktail.idDrink">
          <img src="../assets/placeholder.png" />
          <div>{{cocktail.strDrink}}({{cocktail.idDrink}})</div>
          <ul>
          <div class="cocktail" v-for="(ingredient, index) in cocktail.ingredients" :key="index">
            <li>{{ingredient}}</li>
          </div>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      txtInput: "",
      filteredCocktails: [],
      cocktails: []
    };
  },
  methods: {
    filterData() {
      if (this.txtInput) {
        this.filteredCocktails = this.filteredCocktails.filter(cocktail =>
          cocktail.strDrink.toLowerCase().includes(this.txtInput.toLowerCase())
        );
      }
    }
  },
  computed: {
    filterCocktails: function() {
      const data = this.cocktails.filter(cocktail =>
        cocktail.strDrink.toLowerCase().includes(this.txtInput.toLowerCase())
      );
      return data;
    }
  },
  created() {
    axios
      .get("http://localhost:3000/cocktail")
      .then(response => (this.cocktails = response.data));
  }
};
</script>
<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial;
}

.header {
  text-align: center;
  padding: 32px;
}

.cocktails {
  display: flex;
  flex-wrap: wrap;
  padding: 0 4px;
}


.cocktail {
  flex: 25%;
  max-width: 25%;
  padding: 0 4px;
}

.column img {
  margin-top: 8px;
  vertical-align: middle;
  width: 100%;
}


@media screen and (max-width: 800px) {
  .column {
    -ms-flex: 50%;
    flex: 50%;
    max-width: 50%;
  }
}

@media screen and (max-width: 600px) {
  .column {
    -ms-flex: 100%;
    flex: 100%;
    max-width: 100%;
  }
}
</style>
