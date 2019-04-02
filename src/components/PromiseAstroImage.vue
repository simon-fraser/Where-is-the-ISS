<template>
  <img :src="link" :alt="this.name" />
</template>

<script>
export default {
  name: 'p-img',
  props: {
    name: { type: String, required: true }
  },
  data () {
    return {
      link: ""
    }
  },
  methods: {
    getSrc (name) {
      this.link = `//via.placeholder.com/48?text=${this.name}`
      return fetch(`https://en.wikipedia.org/w/api.php?action=query&origin=*&format=json&formatversion=2&prop=pageimages|pageterms&piprop=thumbnail&pithumbsize=200&titles=${name}`)
        .then((response) => {
          return response.json()
        })
        .then((json) => {
          if (json.query.pages[0].thumbnail.source) this.link = json.query.pages[0].thumbnail.source
        })
    }
  },
  mounted: function () {
    this.getSrc(this.name)
  }
}
</script>
