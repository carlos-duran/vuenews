<template lang="html">
<div class="news-list">
  <h4>Lista de noticias</h4>
  <div class="container">
    <ul class="media-list">
      <li class="media" v-for="article in articles">
        <div class="media-left">
          <a :href="article.url" target="_blank">
            <img :src="article.urlToImage" class="media-object" />
          </a>
        </div>
        <div class="media-body">
          <h4 class="media-heading">
            <a :href="article.url" target="_blank">{{ article.title }}</a>
          </h4>
          <h5><i>by {{ article.author }}</i></h5>
          <p>
            {{ article.description}}
          </p>
        </div>
      </li>
    </ul>
  </div>
</div>
</template>

<script>
export default {
  name: 'NewsList',
  props: ['source'],
  data() {
    return {
      articles: []
    }
  },
  methods: {
    updateSource(source) {
      if(source) {
        this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=d7756e46484b4145966f67512c0fc6c4')
        .then(response => {
          this.articles = response.data.articles
        })

      }
    }
  },
  created() {
    this.updateSource(this.source)
  },
  watch: {
    source: function(val) {
      this.updateSource(val)
    }
  }
}
</script>

<style lang="css" scoped>
  .media-object {
    width: 128px;
    padding: 10px;
  }

  .media {
    border-top: 1px solid lightgrey;
    padding-top: 20px;
  }

</style>
