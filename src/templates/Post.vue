<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + $page.post.image.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
              <span class="meta">
                Posted by
                <a href="#">{{ $page.post.author.name }}</a>
                {{ $page.post.created_at }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="content">
          </div>
        </div>
      </div>
    </article>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  post: strapiArticle(id: $id) {
    id,
    title,
    content,
    created_at,
    image {
      url
    },
    author {
      name,
      id
    },
    categories{
      id,
      name
    }
  }
}
</page-query>
<script>
import MarkDownIt from 'markdown-it'
const md = new MarkDownIt()
export default {
  name: 'PostPage',
  computed: {
    content () {
      return md.render(this.$page.post.content)
    }
  }
}
</script>

<style scoped>
</style>