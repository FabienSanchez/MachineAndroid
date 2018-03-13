<template>
  <div>
    <hr/>
    <button class="btn btn-outline-primary" @click="hideForm = !hideForm"
            v-html="hideForm ? 'Ajouter' : 'Cacher'"></button>
    <div v-if="!hideForm">
      <h4>Ajouter une machine</h4>
      <modal :error="error" :success="success"></modal>
      <form @submit.prevent="onSubmit" class="form-inline mb-3">
        <div class="form-group ">
          <label class="col-sm-2">Nom</label>
          <input v-model="machine.name" class="form-control" type="text" name="name" placeholder="Nom"/>
        </div>
        <div class="form-group">
          <label class="col-sm-2">Lat</label>
          <input v-model="machine.lat" class="form-control" type="number" name="lat"/>
        </div>
        <div class="form-group">
          <label class="col-sm-2">Lng</label>
          <input v-model="machine.lng" class="form-control" type="number" name="lng"/>
        </div>
        <div class="form-check">
          <input v-model="machine.status" class="form-check-input" type="checkbox" id="status" name="status"
                 checked="checked"/>
          <label class="form-check-label" for="status">Status</label>
        </div>
        <button type="submit" class="btn btn-primary">Envoyer</button>
      </form>
    </div>
    <hr/>
  </div>
</template>

<script>
  import modal from './modal.vue'
  import Axios from 'axios'

  export default {
    name: "add-machine",
    props: ['getData'],
    data() {
      return {
        machine: {
          name: '',
          status: true,
          lat: 0,
          lng: 0,
          checkedAt: Date()
        },
        hideForm: true,
        error: null,
        success: null
      }
    },
    methods: {
      onSubmit: function () {
        let self = this;
        self.error, self.success = null;
        self.machine.checkedAt = Date();
        Axios.post('https://machine-api-campus.herokuapp.com/api/machines', self.machine)
          .then(function (response) {
            self.success = true,
              self.getData()

          })
          .catch(function (error) {
            self.error = true
          });
      }
    },
    components: {
      modal
    }
  }
</script>

<style scoped>
  form {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
  }

  .slide-fade-enter-active {
    transition: all .3s ease;
  }

  .slide-fade-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }

  .slide-fade-enter, .slide-fade-leave-to
    /* .slide-fade-leave-active below version 2.1.8 */
  {
    transform: translateX(10px);
    opacity: 0;
  }
</style>
