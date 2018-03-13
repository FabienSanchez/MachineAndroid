<template>
  <div class="container">
    <transition name="slide-fade">
      <div v-if="error" class="alert alert-danger alert-dismissible fade show" role="alert">
        <strong>Attention !</strong> Une erreur est survenue.
        <button type="button" class="close" data-dismiss="alert" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div v-if="success" class="alert alert-success alert-dismissible fade show" role="alert">
        <strong>Félicitation !</strong> Machine ajouté avec succès.
        <button type="button" class="close" data-dismiss="alert" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
    </transition>
  </div>
</template>

<script>
  export default {
    name: "modal",
    props: ['error', 'success']
  }
</script>

<style scoped>

</style>
