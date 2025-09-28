<template>
    <b-navbar type="dark" style="background-color: cornflowerblue;">
    <b-navbar-brand href="#" @click="filterCategory('')">Chirper</b-navbar-brand>
      <b-navbar-nav>
        <b-nav-item href="#" :class="{active : activeCategory === ''}" @click="filterCategory('')">Alle</b-nav-item>
        <b-nav-item href="#" :class="{active : activeCategory === 'featured'}" @click="filterCategory('featured')">Featured</b-nav-item>
        <b-nav-item href="#" :class="{active : activeCategory === 'friends'}" @click="filterCategory('friends')">Freunde</b-nav-item>
      </b-navbar-nav>

      <b-navbar-nav class="ml-auto">
        <b-form-input size="sm" class="mr-4" placeholder="#hashtag suchen" v-model="hashtag" @keydown.enter="filterHashtag"></b-form-input>
        <!-- TODO -->
        <chirp-modal @added-chirp="forwardChirp"></chirp-modal>
      </b-navbar-nav>
  </b-navbar>
</template>

<script>
import CreateChirpModal from './CreateChirpModal.vue'

    export default {
        name: "NavBar",
        data() {
          return {
            activeCategory: '',
            hashtag: ''
          }
        },
        components: {
          'chirp-modal': CreateChirpModal,
        },
        methods: {
          // TODO
          filterCategory(filter){
            this.$emit('filter-chirps', filter);
            this.activeCategory = filter;
            return;
          },
          filterHashtag(){
            if(this.hashtag.startsWith("#")){
              this.$emit('filter-chirps', this.hashtag);
              this.hashtag = '';
              return;
            }
            else {
              this.$emit('filter-chirps', "#" + this.hashtag);
              this.hashtag = '';
              return;
            }
          },
          forwardChirp(newChirp) {
            this.$emit("added-chirp", newChirp);
            return;
          },
        }
    }
</script>

<style scoped></style>