<script>
  const GIPHY_API_KEY = process.env.VUE_APP_GIPHY_API_KEY
  const GIPHY_URL = `https://api.giphy.com/v1/gifs/random?api_key=${GIPHY_API_KEY}&tag=cat&rating=g`
  const CAT_FACT_URL = 'https://catfact.ninja/fact?max_length=140'

  export default {
    data() {
      return {
        gifUrl: null,
        fact: null,
        source: null,
        user: null
      }
    },
    methods: {
      async loadNextMeme() {
        await fetch(GIPHY_URL)
          .then(response => response.json())
          .then(fetched => {
            this.gifUrl = fetched.data.embed_url;
            this.source = fetched.data.source;
            this.user = fetched.data.username;
          });

        await fetch(CAT_FACT_URL)
          .then(response => response.json())
          .then(data => {
            this.fact = data.fact
          });
      }
    },
    async created() {
      await this.loadNextMeme()
    }
  }
</script>

<template>

  <div class="container" style="height: 100vh">

    <div class="row" style="height: 35%">      
      <div class="col">
        <iframe :src="gifUrl" width="100%" height="100%" frameBorder="0" class="rounded"></iframe>
      </div>
    </div>

    <div class="row" style="height: 2.5%">
      <div class="col position-relative">
        <p class="position-absolute top-50 start-50 translate-middle" v-if="Object.keys(user).length != 0">
          Posted on Giphy by <a :href="user">{{user}}</a>
        </p>
      </div>
    </div>

    <div class="row" style="height: 2.5%">
      <div class="col position-relative">
        <p class="position-absolute top-50 start-50 translate-middle" v-if="Object.keys(source).length != 0">
          <a :href="source">Source</a>
        </p>
      </div>
    </div>
    
    <div class="row" style="height: 5%">      
      <div class="col position-relative">
        <img src="@/assets/PoweredByGiphy.png" class="position-absolute top-50 start-50 translate-middle">
      </div>
    </div>

    <div class="row" style="height: 45%">
      <div class="col position-relative">
        <blockquote class="blockquote position-absolute top-50 start-50 translate-middle">
          <p>{{fact}}</p>
          <footer class="blockquote-footer">Fact by <a href="https://catfact.ninja/">catfact.ninja</a></footer>
        </blockquote>
      </div>
    </div>

    <div class="row position-relative" style="height: 10%">
      <div class="col">
        <button class="btn btn-danger position-absolute top-0 start-50 translate-middle" @click="loadNextMeme">
          Next!
        </button>
      </div>
    </div>

  </div>
  
</template>