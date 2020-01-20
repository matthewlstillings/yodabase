<template>
  <div id="modal" :class="`${selectedData ? 'open' : 'closed'} wrapper`">
    <a class="close" @click="$emit('handleSelectedData', null)">X</a>
    <div class="content">
      <div>
        <div class="modal_datum" v-for="(value, index) in selectedData" :key="value">
          <p class="key">{{index.replace(/_/g, " ")}}</p>
          <p class="value">{{value}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: ["selectedData"]
};
</script>

<style lang="scss">
#modal {
  background: rgba(0, 0, 0, 0.7);
  top: 0;
  left: 0;
  height: 100%;
  position: fixed;
  width: 100%;
  &.open {
    display: block;
  }
  &.closed {
    display: none;
  }
  &.people_modal {
    .modal_datum:nth-last-child(-n + 8) {
      display: none;
    }
  }
  &.people_modal {
    .modal_datum:nth-last-child(-n + 8) {
      display: none;
    }
  }
  &.planets_modal {
    .modal_datum:nth-last-child(-n + 5) {
      display: none;
    }
  }
  &.films_modal {
    .modal_datum:nth-last-child(-n + 8) {
      display: none;
    }
  }
  &.species_modal {
    .modal_datum:nth-last-child(-n + 7) {
      display: none;
    }
  }
  &.vehicles_modal {
    .modal_datum:nth-last-child(-n + 5) {
      display: none;
    }
  }
  &.starships_modal {
    .modal_datum:nth-last-child(-n + 6) {
      display: none;
    }
  }
  .content {
    background: white;
    left: 50%;
    max-height: 500px;
    overflow-y: scroll;
    max-width: 700px;
    padding: 2rem 1rem;
    position: relative;
    transform: translate(-50%);
    top: 20%;
    width: 95%;
  }
  .modal_datum {
    border-top: 1px solid black;
    padding: 0.5rem;
    .key {
      color: darken(#ffe81f, 14%);
      font-size: 1.1rem;
      margin-bottom: 0.5em;
      text-decoration: underline;
      text-transform: capitalize;
    }
    .value {
      color: black;
      text-transform: capitalize;
    }
  }
  .modal_datum:nth-child(1) {
    border-top: none;
  }
  .close {
    cursor: pointer;
    font-size: 2rem;
    left: 50%;
    position: absolute;
    top: 4rem;
    transform: translate(-50%);
  }
}
</style>