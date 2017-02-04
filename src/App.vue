<template>
  <div class="container" id="app">
    <source-selection @sourceChanged="sourceChanged"></source-selection>
    <news-list :source="source"></news-list>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection.vue'
import NewsList from './components/NewsList.vue'

export default {
  name: 'app',
  components: {
    SourceSelection,
    NewsList
  },
  data() {
    return {
      source: ''
    }
  },
  methods: {
    sourceChanged(source) {
      this.source = source;
    }
  }
}
</script>

<style>
  #app {
    padding-top: 20px;
  }
</style>
