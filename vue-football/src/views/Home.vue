<script>
  import NavBar from '../components/NavBar.vue' ;
  import Card from '../components/Card.vue';
  import { mapActions, mapState } from 'pinia';
  import { useFootballStore } from '../stores/football';

  export default {
    name: "home",

    components: {
      NavBar,
      Card
    },

    methods: {
      ...mapActions(useFootballStore, ["fetchLiveFootball"])
    },
    computed: {
      ...mapState(useFootballStore, ["liveData"])
    },
    created() {
      this.fetchLiveFootball();
    }
  }
</script>

<template>
  <NavBar />
  <div class="container mb-4">
    <div style="margin-top: 4.5em">
      <h3 class="text-center">Live Score</h3>
    </div>
    <hr>
    <!-- <pre>{{liveData}}</pre> -->
    <h4 v-if="liveData.length === 0" class="card-title" style="text-align: center;">Sorry, there is no live match now <i class="bi bi-emoji-frown"></i></h4>
    <div class="row mb-4">
      <Card 
        v-for="football in liveData"
        :key="football.id"
        :football="football"
      />
    </div>
  </div>
</template>