<template>
  <Layout>
    <h1>{{ $page.category.name }}</h1>
    <ul>
      <li v-for="article in $page.category.articles" :key="article.id">
        <g-link :to="'/post/' + article.id">
          {{ article.title }}
        </g-link>
      </li>
    </ul>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  category: strapiCategory(id: $id) {
    name
    articles {
      id,
      title,
    }
  }
}
</page-query>

<script>
export default {
  name: 'Tag'
}
</script>
