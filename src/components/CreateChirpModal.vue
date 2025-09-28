<template>
  <div>
    <b-button v-b-modal.modal-1 size="sm" variant="outline-light">Chirpen!</b-button>
    <b-modal id="modal-1" title="Neuen Chirp erstellen" @ok="addChirp">

      <!-- TODO -->
      <b-form-group
        id="name"
        label="Dein Name *"
        label-for="input-1"
      >
        <b-form-input id="input-1" v-model="newChirp.author"></b-form-input>
      </b-form-group>

      <b-form-group
        id="message"
        label="Deine Nachricht *"
        label-for="input-2"
        :description="numberOfCharacters"
      >
        <b-form-textarea
          id="textarea"
          v-model="newChirp.text"
          placeholder="max. 200 Zeichen"
          max-rows="5"
          @keydown="maxChars"
        ></b-form-textarea>
      </b-form-group>

      <b-form-group
        id="hashtag"
        label="Hashtags:"
        label-for="input-3"
        description="Hashtags durch Leerzeichen getrennt angeben"
      >
        <b-form-input id="input-3" v-model="hashtagString" placeholder="z.B. #hashtag1 #hashtag2"></b-form-input>
      </b-form-group>

    </b-modal>
  </div>
</template>

<script>
export default {
  name: "CreateChirpModal",
  data() {
    return {
      hashtagString: "",
      newChirp: {
        author: "",
        text: "",
        hashtags: [],
      },
    };
  },
  computed: {
    numberOfCharacters() {
      var length = 200 - this.newChirp.text.length;
      return "Noch " + length.toString() + " Zeichen übrig";
    }
  },
  methods: {
    addChirp(bvModalEvt) {
      if (this.newChirp.author && this.newChirp.text) {
        this.newChirp.hashtags = this.hashtagString
          .split(" ")
          .map((h) => "#" + h.replace("#", ""));
        this.$emit("added-chirp", this.newChirp);
        return;
      } else {
        bvModalEvt.preventDefault();
        return;
      }
    },
    maxChars(event) {
      if(this.newChirp.text.length > 200){
        this.newChirp.text = this.newChirp.text.substring(0, 200);
      }
      if(this.newChirp.text.length >= 200 && event.keyCode != 8){
        event.preventDefault();
        return;
      }
    },
  },
};
</script>

<style scoped>
</style>