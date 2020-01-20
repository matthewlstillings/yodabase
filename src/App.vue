<template>
  <div id="app">
    <h1 class="app_title">YodaBase</h1>
    <p class="app_subtitle">A database for Star Wars information</p>
    <Search
      @handleParamChange="handleParamChange"
      @handleCategoryChange="handleCategoryChange"
      @fetchData="fetchData"
    />
    <List v-bind:results="results" v-bind:error="error" @handleSelectedData="handleSelectedData" />
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
    return {
      results: null,
      urlCategory: "films",
      searchParams: "Params",
      selectedData: null,
      error: false
    };
  },
  methods: {
    fetchData(event) {
      event.preventDefault();
      this.error = false;
      const dataUrl = `https://swapi.co/api/${this.urlCategory}/?search=${this.searchParams}`;
      fetch(dataUrl)
        .then(response => response.json())
        .then(data => {
          if (data.results.length === 0) {
            this.error = !this.error;
            this.results = [];
          } else {
            this.results = data.results;
            this.listKey = Object.keys(data.results[0]).map(category => {
              return category.replace(/_/g, " ");
            });
          }
        });
    },
    handleCategoryChange(category) {
      this.urlCategory = category;
    },
    handleParamChange(params) {
      this.searchParams = params;
    },
    handleSelectedData(data) {
      this.selectedData = data;
    }
  },
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
  font-size: 16px;
  padding: 5rem 1.5rem 1.5rem;
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
</style>
