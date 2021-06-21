<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h3>{{ post.title }}</h3>
    <p class="pre">{{ post.body }}</p>
  </div>
  <div v-else>
    <Spinner />
  </div>
</template>

<script>
import Spinner from '@/components/Spinner'
import getPost from '@/actions/getPost'
import { useRoute } from 'vue-router'

export default {
  name: 'Detail',
  props: {
    id: Number
  },
  components: {
    Spinner
  },
  setup(props) {
    const route = useRoute()
    const { error, post, load } = getPost(route.params.id)

    load()

    return {
      post,
      error,
    }
  }
}
</script>

<style scoped>
.post {
  max-width: 1200px;
  margin: 0 auto;
}
.post p {
  color: #444;
  line-height: 1.5em;
  margin-top: 40px;
}
.pre {
  white-space: pre-wrap;
}
</style>