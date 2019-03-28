<template>
  <div class="detpanel">
    <header class="container grid-md mb-2">
      <h2>Some Additional Information</h2>
    </header>
    <div class="container grid-md">
      <div class="columns">
        <div class="column col-md-6">
          <h3>Current Crew</h3>
            <ul>
              <li v-for="cx in crew" :key="cx.name">
                <span>
                  <figure class="avatar avatar-lg mr-2">
                    <img :src="getCrewImage(cx.name.replace(' ', '_'))" alt="...">
                  </figure>
                  <a :href="`https://en.wikipedia.org/wiki/${ cx.name.replace(' ', '_') }`" target="_blank">{{ cx.name }}</a>
                </span>
              </li>
            </ul>

        </div>
        <div class="column col-md-6">col--6</div>
      </div>
    </div>
  </div>
</template>

<style>
  .detpanel {
    padding: 20px 0 40px;
  }
</style>

<script>

export default {
  name: 'issdetails',
  data () {
    return {
      crew: []
    }
  },
  methods: {
    getCrew () {
      fetch('http://api.open-notify.org/astros.json') // process.env.VUE_APP_ISS_POSITION
        .then((response) => {
          return response.json()
        })
        .then((json) => {
          if (json.message === "success") this.crew = json.people
        })
    },
    async getCrewImage (name) {
      return fetch(`https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&formatversion=2&prop=pageimages|pageterms&piprop=thumbnail&pithumbsize=200&titles=${name}`)
        .then((response) => {
          return response.json()
        })
        .then((json) => {
          if (json.query.pages[0].thumbnail.source) return json.query.pages[0].thumbnail.source
        })
    }
  },
  async mounted() {
    await this.getCrew()
  }
}
</script>