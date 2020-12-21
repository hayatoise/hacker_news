<template>
  <div>
    <article>
      <a :href="article.url">
        <h2>{{ article.title }}</h2>
        <hr />
      </a>
    </article>
  </div>
</template>

<script>
export default {
  props: {
    article: {
      type: Array,
      required: true,
    },
  },
}
</script>
