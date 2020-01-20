<template>
  <div id="search_contain" class="contain">
    <form @submit="$emit('fetchData', $event)">
      <select class="search_select" @change="$emit('handleCategoryChange', $event.target.value)">
        <option value="films">Films</option>
        <option value="people">People</option>
        <option value="planets">Planets</option>
        <option value="species">Species</option>
        <option value="starships">Starships</option>
        <option value="vehicles">Vehicles</option>
      </select>
      <input
        type="text"
        class="search_input"
        placeholder="Data, you seek?"
        @keyup="$emit('handleParamChange', $event.target.value)"
      />
      <button class="search_submit" type="submit">Search</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Search",
  props: ["urlCategory"]
};
</script>

<style lang="scss">
form {
  display: flex;
  margin: auto;
  max-width: 700px;
}
.search_submit,
.search_input,
.search_select {
  border: none;
  box-shadow: none;
  color: black;
  font-family: "Roboto", sans-serif;
  height: 32px;
  -webkit-appearance: none;
  font-size: 16.5px;
}
.search_input {
  padding: 0.5em;
  border-radius: 0;
  width: 50%;
}
.search_select {
  background: lighten(#ffe81f, 15%);
  border-radius: 5px 0px 0px 5px;
  border-right: 1px solid black;
  cursor: pointer;
  padding: 0 0.5em;
  text-align: center;
  transition: background-color 0.3s ease;
  width: 25%;
}
.search_select:hover {
  background: darken(#ffe81f, 15%);
}
.search_select:focus {
  font-size: 16.5px;
}
option {
  border-bottom: 1px solid black;
  background: white;
}
.search_submit {
  background: #ffe81f;
  border-radius: 0px 5px 5px 0px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  width: 25%;
  border-left: 1px solid black;
}
.search_submit:hover {
  background: darken(#ffe81f, 15%);
}
</style>