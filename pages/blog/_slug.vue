<template>
  <div v-if="posts.length < 1">
    <p>loading</p>
  </div>
  <main
    v-else
    class="post individual"
  >
    <h1>{{ post.title.rendered }}</h1>
    <small class="date">{{ post.date | dateformat }}</small>
    <section v-html="post.content.rendered" />
  </main>
</template>

<script>
export default {
  data () {
    return {
      slug: this.$route.params.slug
    }
  },
  computed: {
    posts () {
      return this.$store.state.posts
    },
    post () {
      return this.posts.find(el => el.slug === this.slug)
    }
  },
  created () {
    this.$store.dispatch('getPosts')
  }
}
</script>
