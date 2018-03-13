<template>
  <div>
    <h4>Filtre</h4>
    <div class="filter-group btn-group btn-group-toggle" data-toggle="buttons">
      <label @click="setFilter(null)" for="option1" :class="{ active: filter==null }" class="btn btn-outline-primary">
        <input type="radio" name="options" id="option1" autocomplete="off">
        All
      </label>
      <label @click="setFilter(true)" for="option2" :class="{ active: (filter==true) }" class="btn btn-outline-success">
        <input type="radio" name="options" id="option2" autocomplete="off">
        Ok
      </label>
      <label @click="setFilter(false)" for="option3" :class="{ active: (filter==false) }"
             class="btn btn-outline-danger">
        <input type="radio" name="options" id="option3" autocomplete="off">
        Ko
      </label>
    </div>
  </div>
</template>

<script>
  export default {
    name: "filtre",
    props: ['filter', 'setFilter']
  }
</script>

<style scoped>

</style>
