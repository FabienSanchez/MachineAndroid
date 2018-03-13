<template>
  <div>
    <gmap-map
      class="map"
      :center="center"
      :zoom="2"
      map-type-id="hybrid"
    >
      <gmap-marker
        v-for="(machine) in machines"
        v-if="
        (filter==null) ||
        (filter==false && machine.status=='false') ||
        (filter==true && machine.status=='true')"
        :key="machine.id"
        :position="toLatIng(machine)"
        :clickable="true"
        @click="center=toLatIng(machine)"
      >
      </gmap-marker>
    </gmap-map>
  </div>
</template>

<script>
  export default {
    name: "machines-map",
    props: ['machines', 'filter'],
    data() {
      return {
        center: {lat: 45.1666700, lng: 5.7166700}
      }
    },
    methods: {
      toLatIng: function (machine) {
        let lat = Number(machine.latitude);
        let lng = Number(machine.longitude);
        return {lat: lat, lng: lng}
      }
    },
    created() {
      let self = this;
      navigator.geolocation.getCurrentPosition(function (position) {
        self.center = {lat: position.coords.latitude, lng: position.coords.longitude}
      });
    }
  }
</script>

<style scoped>
  .map {
    width: auto;
    height: 800px;
    margin: 5px;
  }
</style>
