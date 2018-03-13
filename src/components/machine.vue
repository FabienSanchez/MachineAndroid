<template>
  <div>
    <div class="col-md-10">
      <h1>{{ machine.name }}</h1>
      <div v-bind:class="etat ? 'text-success' : 'text-danger'">
        Status :
        <span v-html="etat ? 'OK' : 'KO'"></span>
        <toggle-button :sync="true" :labels="true" :value=etat @change="update(machine)"/>
      </div>
      <br/>
      <p>Last time checked : {{ machine.checkedAt }} </p>
    </div>
    <div class="align-btn col-md-2">
      <button @click="supprimer(machine.id, machine.name)" type="button" class="btn btn-outline-danger"
              data-toggle="modal"
              data-target="#supprimer"
      >Supprimer
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "machine",
    props: ['machine', 'supprimer', 'setStatus', 'update'],
    computed: {
      etat: function () {
        if (this.machine.status == "true") {
          return true
        } else {
          return false
        }
      }
    },
  }
</script>

<style scoped>
  .align-btn {
    margin: auto;
    padding: 10px;
  }
</style>
