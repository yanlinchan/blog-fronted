<template>
  <Layout>
    

    <!-- Page Header -->
    <header
      class="masthead"
      :style="{backgroundImage: `url(${GRIDSOME_API_URL + general.shareImage.url})`}"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ general.metaTitle }}</h1>
              <span class="subheading">{{ general.metaDescription }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">{{ edge.node.title }}</h2>
              <!-- <h3 class="post-subtitle">Problems look mighty small from 150 miles up</h3> -->
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#">{{ edge.node.author.name }}</a>
              on {{ edge.node.created_at }}
            </p>
            <p>
              <span v-for="tag in edge.node.categories" :key="tag.id">
                <g-link :to="'/tag/' + tag.id">{{ tag.name }}</g-link>&nbsp;&nbsp;
              </span>
            </p>
          </div>
          <hr />
          <!-- <div class="post-preview">
            <a href="post.html">
              <h2
                class="post-title"
              >I believe every human has a finite number of heartbeats. I don't intend to waste any of mine.</h2>
            </a>
            <p class="post-meta">
              Posted by
              <a href="#">Start Bootstrap</a>
              on September 18, 2019
            </p>
          </div>
          <hr />
          <div class="post-preview">
            <a href="post.html">
              <h2 class="post-title">Science has not yet mastered prophecy</h2>
              <h3 class="post-subtitle">We predict too much for the next year and yet far too little for the next ten.</h3>
            </a>
            <p class="post-meta">
              Posted by
              <a href="#">Start Bootstrap</a>
              on August 24, 2019
            </p>
          </div>
          <hr />
          <div class="post-preview">
            <a href="post.html">
              <h2 class="post-title">Failure is not an option</h2>
              <h3
                class="post-subtitle"
              >Many say exploration is part of our destiny, but it’s actually our duty to future generations.</h3>
            </a>
            <p class="post-meta">
              Posted by
              <a href="#">Start Bootstrap</a>
              on July 8, 2019
            </p>
          </div>
          <hr /> -->
          <!-- Pager -->
          <div class="clearfix">
            <!-- <a
              class="btn btn-primary float-right"
              href="#"
            >Older Posts &rarr;</a> -->
            <Pager :info="$page.posts.pageInfo"></Pager>
          </div>
        </div>
      </div>
    </div>

    
  </Layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiArticle (perPage: 2, page: $page) @paginate {
    pageInfo {
      perPage,
      currentPage,
      totalPages,
      totalItems,
      hasPreviousPage,
      hasNextPage,
      isFirst,
      isLast
    }
    edges {
      node {
        id,
        title,
        created_at,
        author {
          id,
          name
        },
        categories {
          name,
          id
        }
      }
    }
  }
  allStrapiHomePage {
    edges {
      node {
        seo {
          metaTitle,
          metaDescription,
          shareImage {
            url
          }
        }
      }
    }
  }
}
</page-query>
<script>
import { Pager } from 'gridsome'
export default {
  metaInfo: {
    title: 'Hello, world!'
  },
  name: 'HomePage',
  components: {
    Pager
  },
  computed: {
    general () {
      return this.$page.allStrapiHomePage.edges[0].node.seo
    }
  },
}
</script>

<style>
</style>
