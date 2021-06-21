<template>
  <div class="tag">
    <div v-if="error">{{ error }}</div>
    <div v-if="posts.length" class="layout">
      <PostList :posts="postsWithTag" />
      <TagList :posts="posts" />
    </div>
    <div v-else>
      <Spinner />
    </div>
  </div>
</template>

<script>
import TagList from '@/components/TagList.vue'
import Spinner from '@/components/Spinner.vue'
import PostList from '@/components/PostList.vue'
import getPosts from '@/actions/getPosts'

import { useRoute } from 'vue-router'
import { computed } from 'vue'

export default {
  name: 'Tag',
  components: {
    PostList,
    Spinner,
    TagList
  },
  setup() {
    const router = useRoute()
    const { posts, error, load } = getPosts()

    load()

    const postsWithTag = computed(() => {
      return posts.value.filter(p => p.tags.includes(router.params.tag))
    })

    return {
      router,
      posts,
      error,
      postsWithTag,
    }
  }
}
</script>

<style scoped>
.tag {
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px;
}
.layout {
  display: grid;
  grid-template-columns: 3fr 1fr;
  gap: 20px;
}
</style>