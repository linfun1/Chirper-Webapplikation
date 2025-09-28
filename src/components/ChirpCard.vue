 <template>
  <b-col cols="12" sm="12" md="6" lg="4" xl="4">
    <b-card class="mt-3 mb-2 flex-row">
      <b-row>
        <b-col cols="2" class="p-0 m-0">
          <b-card-img :src="getImgUrl(chirp.thumbnail)" class="rounded-circle p-0" style="margin"></b-card-img>
        </b-col>
        <b-col cols="10" class="p-0 mt-0">
          <b-card-body class="pt-0 pb-0 pl-10">
            <b-card-title v-text="chirp.author"></b-card-title>
            <b-card-text>
              <span>{{chirp.text}} </span>
              <span style="color: cornflowerblue;" v-for="hashtag in chirp.hashtags" v-bind:key="hashtag">{{hashtag}} </span>
            </b-card-text>
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </b-col>
</template>

<script>
export default {
  name: "ChirpCard",
  methods: {
    getImgUrl(thumbnailPath) {
      return require("../assets/" + thumbnailPath);
    },
    // TODO
  },
  props: {
        chirp: {
            type: Object,
            required: true
        }
    },
};
</script>

<style scoped>

</style>