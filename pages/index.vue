<template>
  <div>
    <h1 class="website-title">Hacker News</h1>
    <div v-for="article in articles" :key="article.id">
      <Article :article="article" />
    </div>
  </div>
</template>

<script>
import Article from '../components/Article'

export default {
  components: {
    Article,
  },
  async asyncData({ $axios }) {
    const topStoryIds = await $axios.$get(
      'https://hacker-news.firebaseio.com/v0/topstories.json'
    )

    const topTenIds = topStoryIds.filter(
      (topStoryId) => topStoryIds.indexOf(topStoryId) <= 10
    )

    const articles = []
    let articleId
    for (articleId in topTenIds) {
      const itemUrl = `https://hacker-news.firebaseio.com/v0/item/${articleId}.json?print=pretty`
      const item = await $axios.$get(itemUrl)
      if (item) {
        articles.push(item)
      }
    }

    return {
      articles,
    }
  },
}
</script>

<style scoped>
.website-title {
  margin: 16px 16px;
  font-size: calc(1rem + 1vw);
  font-weight: bold;
}
</style>
