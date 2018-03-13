<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-sm-12">
        <img id="logo" src="./assets/coffe-cup.jpg">
        <div class="jumbotron">
          <h1>{{ msg }}</h1>
          <h2>que faire ?</h2>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12">
        <ul class="nav nav-tabs nav-fill">
          <li class="nav-item">
            <router-link to="/machines" class="nav-link">Liste</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/map" class="nav-link">Map</router-link>
          </li>
        </ul>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12">
        <div class="tabs-container">
          <div id="loading" v-if="loading"><img id="loader" src="./assets/3.gif"/>Loading</div>
          <div v-else-if="error">
            <h1 class="text-danger">Erreur {{ error.response.status}}</h1>
            <p class="text-danger">{{ error.response.statusText}}</p>
          </div>
          <div v-else-if="responseStatus">
            <form-machine :getData="getData" ></form-machine>
            <filtre :filter="filter" :setFilter="setFilter"></filtre>
            <confirm-delete :machine="aSupprimer" :confirmDelete="confirmDelete"></confirm-delete>
            <router-view :supprimer="supprimer" :machines="machines" :filter="filter" :setStatus="setStatus"
                         :update="update"></router-view>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Axios from 'axios'
  import filtre from './components/filtre.vue'
  import confirmDelete from './components/confirmDelete.vue'
  import formMachine from './components/addMachine.vue'

  export default {
    name: 'app',
    data() {
      return {
        msg: 'Coffee Machine Vader',
        machines: [],
        loading: true,
        error: null,
        responseStatus: false,
        filter: null,
        aSupprimer: {}
      }
    },
    methods: {
      setFilter: function (value) {
        this.filter = value;
      },
      getData: function () {
        Axios.get('https://machine-api-campus.herokuapp.com/api/machines')
          .then((response) => {
            if (response.status == 200) {
              this.machines = response.data;
              this.responseStatus = true;
            }
            this.loading = false;
          })
          .catch((error) => {
            this.loading = false;
            this.error = error;
          });
      },
      supprimer: function (id, nom) {
        this.aSupprimer = {id: id, name: nom}
      },
      confirmDelete: function () {
        let self = this
        Axios.delete('https://machine-api-campus.herokuapp.com/api/machines/' + self.aSupprimer.id)
          .then(function (response) {
            self.getData()
          })
          .catch(function (error) {
          });
      },
      update: function (object) {
        let self = this
        if (object.status == "true") {
          object.status = "false"
        } else {
          object.status = "true"
        }
        Axios.put('https://machine-api-campus.herokuapp.com/api/machines/' + object.id, {
          status: object.status,
          id: object.id,
          name: object.name,
          longitude: object.longitude,
          latitude: object.latitude,
          checkedAt: object.checkedAt
        })
          .then(function (response) {
            self.getData()
          })
      },
      setStatus: function (object) {
        if (object.status == "true") {
          object.status = true
        } else {
          object.status = false
        }
      },
    },
    created() {
      this.getData()
    },
    components: {
      filtre,
      formMachine,
      confirmDelete
    }
  }
</script>

<style>
  @media (max-width: 768px) {
    .container {
      max-width: 97.5%;
      padding-left: none;
      padding-right: none;
    }
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  #logo {
    padding: 10px;
  }

  #loading {
    font-size: 2em;
  }

  #loader {
    width: 40px;
    height: 40px;
  }

  img {
    width: 200px;
    height: 200px;
  }

  .tabs-container {
    border-bottom-left-radius: .25rem;
    border-bottom-right-radius: .25rem;
    border: 1px solid transparent;
    border-color: transparent #dee2e6 #dee2e6 #dee2e6;
  }

  .filter-group {
    padding: 10px;
  }

  .filter-group > * {
    margin: auto;
  }

  h1, h2 {
    font-weight: normal;
  }

  h1 {
    color: #53240f;
    overflow-wrap: break-word;
  }

  h2 {
    color: chocolate;
  }

  .nav-link {
    background: rgba(200, 200, 200, 0.1);

  }

  a, a:hover {
    font-size: 1.5em;
    color: inherit;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }
</style>
