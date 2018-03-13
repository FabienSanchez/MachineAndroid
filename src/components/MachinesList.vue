<template>
  <div>
    <div class="machinesCont"
         v-if="
         (filter==null) ||
         (filter==false && machine.status=='false') ||
         (filter==true && machine.status=='true')"
         v-for="machine in machines">
      <machine :supprimer="supprimer" :machine="machine" :key="machine.id" :setStatus="setStatus"
               :update="update" class="machines row"/>
    </div>
  </div>
</template>

<script>
  import Machine from './Machine.vue'

  export default {
    name: "machines-list",
    props: ['machines', 'filter', 'supprimer', 'setStatus', 'update'],
    components: {
      Machine
    }
  }
</script>

<style scoped>

  .row {
    margin: auto;
  }
  .machines {
    border: 1px solid #dee2e6;
    border-radius: .25rem;
  }

  .machinesCont {
    border-radius: .25rem;
    margin: 10px;
  }

  .machinesCont:nth-child(odd) {
    background: rgba(125, 125, 125, 0.1);
  }

</style>
