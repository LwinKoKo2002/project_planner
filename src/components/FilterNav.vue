<template>
  <nav class="main-nav">
    <button @click="clickHandler('all')" :class="{ active: current === 'all' }">
      all
    </button>
    <button
      @click="clickHandler('complete')"
      :class="{ active: current === 'complete' }"
    >
      complete
    </button>
    <button
      @click="clickHandler('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    clickHandler(value) {
      console.log(value);
      this.$emit("filterBy", value);
    },
  },
};
</script>

<style>
.main-nav button {
  border: none;
  background-color: white;
  color: #777;
  outline: none;
  margin-right: 10px;
  cursor: pointer;
}
.main-nav button.active {
  color: black;
}
</style>