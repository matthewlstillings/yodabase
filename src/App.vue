<template>
  <div id="app">
    <h1 class="app_title">YodaBase</h1>
    <p class="app_subtitle">A database for Star Wars information</p>
    <Search
      @handleParamChange="handleParamChange"
      @handleCategoryChange="handleCategoryChange"
      @fetchData="fetchData"
    />
    <List
      v-bind:results="results"
      v-bind:error="error"
      v-bind:loading="loading"
      @handleSelectedData="handleSelectedData"
    />
    <Modal
      :class="`${urlCategory}_modal`"
      v-bind:selectedData="selectedData"
      @handleSelectedData="handleSelectedData"
    />
  </div>
</template>

<script>
import Search from "./components/Search";
import List from "./components/List";
import Modal from "./components/Modal";

export default {
  name: "YodaBase",
  components: {
    Search,
    List,
    Modal
  },
  data: function() {
    //"state"
    return {
      results: null, //stores results
      urlCategory: "films", //stores category in which to search database with
      searchParams: "", //stores search paras to build URL
      selectedData: null, //stores "featured" data that goes into modal
      error: false, //sets to to true if search returns nothing
      loading: false //sets to true while returning results
    };
  },
  methods: {
    //fetches data when user searches
    fetchData(event) {
      event.preventDefault();
      this.results = []; //clear results on new search
      this.error = false; //will set error to false is previous search returns no results
      this.loading = true; //initiates loading screen
      const dataUrl = `https://swapi.co/api/${
        this.urlCategory
      }/?search=${encodeURIComponent(this.searchParams)}`;
      fetch(dataUrl)
        .then(response => response.json())
        .then(data => {
          if (data.results.length === 0) {
            //if no data returns, set error
            this.error = !this.error;
            this.results = [];
            this.loading = false;
          } else {
            //if data returns, set results
            this.results = data.results;
            this.loading = false; //ends loading screen
          }
        });
    },
    //change category (for url build) to search in from select element
    handleCategoryChange(category) {
      this.urlCategory = category;
    },
    //change search params for url build
    handleParamChange(params) {
      this.searchParams = params;
    },
    //set "featured" data for modal
    handleSelectedData(data) {
      this.selectedData = data;
    }
  },
  //watches for data changes on these functions
  watch: {
    value: function() {
      this.handleParamChange();
      this.handleSelectedData();
    }
  }
};
</script>

<style lang="scss">
@font-face {
  font-family: "DistantWorlds";
  src: url("./assets/font/SfDistantGalaxyOutline-xoeO.ttf");
  font-style: normal;
}
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background: #232323;
  font-size: 14px;
  padding: 5rem 0.5rem 1.5rem;
  color: white;
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

h1 {
  color: #ffe81f;
  font-family: "DistantWorlds";
  font-size: 3rem;
  margin-bottom: 0.5rem;
}
.app_subtitle {
  margin-bottom: 1rem;
}
@media (min-width: 767px) {
  body {
    font-size: 18px;
  }
}
</style>
