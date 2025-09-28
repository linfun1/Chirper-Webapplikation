<template>
  <b-container>
    <b-row align-h="start">
        <!--<b-card-group>-->
            <!--<b-col>-->
              <chirp-card v-for="chirp in chirps" v-bind:key="chirp.id" v-bind:chirp="chirp"></chirp-card>
            <!--</b-col>-->
        <!--</b-card-group>-->
    </b-row>
  </b-container>
</template>

<script>
import ChirpCard from './ChirpCard.vue';

export default {
  name: "ChirpContainer",
  //TODO
  components: {
        'chirp-card': ChirpCard,
    },
  props: {
    chirps: {
      type: Array,
      required: true,
    }
  }
};
</script>

<style scoped>

</style>