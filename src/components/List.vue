<template>
  <div id="results" class="contain">
    <div
      @click="$emit('handleSelectedData', result)"
      v-for="(result) in results"
      :key="result.name"
      class="result"
    >
      <p>{{result.name}}{{result.title}}</p>
      <p>Read more...</p>
    </div>
    <div class="no_results" v-if="error">
      <p>Sorry, these are not the droids you were looking for.</p>
    </div>
    <Loader v-if="loading" />
  </div>
</template>

<script>
import Loader from "./Loader";
export default {
  name: "List",
  props: ["results", "error", "loading"],
  components: {
    Loader
  }
};
</script>

<style lang="scss">
#results {
  margin: 2em auto 0;
  max-width: 800px;
  .result {
    border-bottom: 0.5px solid white;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    padding: 1rem 0;
  }
  .result:nth-last-child(1) {
    border-bottom: none;
  }
  .result:hover {
    color: #ffe81f;
  }
  .no_results p {
    color: #ffe81f;
    font-family: "DistantWorlds";
    font-size: 1.4rem;
  }
}
</style>