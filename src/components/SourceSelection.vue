<template lang="html">
  <div class="source-selection">
    <div class="jumbotron">
      <h1><span class="glyphicon glyphicon-list-alt"></span> Noticias</h1>
      <h4>Selecciona la fuente de noticias</h4>
      <select class="form-control" @change="sourceChanged">
        <option v-for="source in sources" :value="source.id">{{ source.name }}</option>
      </select>

      <div class="" v-if="source">
        <h6>{{ source.description }}</h6>
        <a :href="source.url" class="btn btn-primary" target="_blank">Go To {{ source.name }}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SourceSelection',
  data() {
    return {
      source: '',
      sources: []
    }
  },
  methods: {
    sourceChanged(e) {
      for (var i = 0; i < this.sources.length; i++) {
        if(this.sources[i].id == e.target.value) {
          this.source = this.sources[i]
        }
      }
      this.$emit('sourceChanged', e.target.value)
    }
  },
  created() {
    this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then(response => {
        this.sources = response.data.sources
        this.$emit('sourceChanged', response.data.sources[0].id)
      })
  }
}
</script>

<style lang="css">
</style>
