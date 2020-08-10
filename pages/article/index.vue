<template>
  <div class="container">
    <button @click="getPosts">get post</button>
    <h1>{{ ip }}</h1>
    <h1>Blog posts</h1>
    <!-- <p v-if="$fetchState.pending">Fetching posts...</p>
    <p v-else-if="$fetchState.error">Error while fetching posts: {{ $fetchState.error.message }}</p> -->
    <ul v-if="posts.length > 0">
      <li v-for="post of posts" :key="post.id">
        <n-link :to="`/posts/${post.id}`">{{ post.title }}</n-link>
      </li>
    </ul>
    <div v-else>no thing</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: 'Hello World!',
      posts: []
    }
  },
  head () {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        { hid: 'description', name: 'description', content: 'My custom description' }
      ]
    }
  },
  async asyncData({ $axios }) {
    const ip = await $axios.$get('http://icanhazip.com')
    return { ip }
  },
  // async fetch () {
  //   let res = await this.$axios.get('https://jsonplaceholder.typicode.com/posts')
  //   this.posts = res.data
  //   console.log(res.data)
  // },
  methods:{
    async getPosts(){
      let res = await this.$axios.get('https://jsonplaceholder.typicode.com/posts')
      this.posts = res.data
    }
  }
}
</script>

<style lang="postcss">
/* Sample `apply` at-rules with Tailwind CSS */
.container {
  @apply min-h-screen flex justify-center flex-col items-center text-center mx-auto ;
}
.box1 {
  @apply text-center transition ease-in-out duration-300
}
</style>
