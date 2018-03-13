<template>
  <div class="modal fade" id="supprimer" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
       aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Êtes vous sûr de vouloir supprimer {{ machine.name }} ?</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-danger" data-dismiss="modal">Cancel</button>
          <button @click="confirmDelete" type="button" class="btn btn-success" data-dismiss="modal">Confirm</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "confirm-delete",
    props: ['confirmDelete', 'machine'],
  }
</script>

<style scoped>

</style>
