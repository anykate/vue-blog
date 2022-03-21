<template>
  <div class="create">
    <form @submit.prevent="handleSubmit">
      <label for="title">Title</label>
      <input v-model="title" type="text" name="title" id="title" required />

      <label for="body">Content</label>
      <textarea v-model="body" name="body" id="body" required />

      <label for="tags">Tags (hit enter to add a tag)</label>
      <input
        @keydown.enter.prevent="handleKeyDown"
        v-model="tag"
        type="text"
        name="tags"
        id="tags"
      />

      <div v-for="tag in tags" :key="tag" class="pill">#{{ tag }}</div>

      <button>Add Post</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

export default {
  name: 'Create',
  setup() {
    const title = ref('')
    const body = ref('')
    const tags = ref([])
    const tag = ref('')

    const router = useRouter()

    const handleKeyDown = () => {
      if (!tags.value.includes(tag.value)) {
        tag.value = tag.value.replace(/\s/g, '') // remove all whitespace
        tags.value.push(tag.value)
      }
      tag.value = ''
    }

    const handleSubmit = async () => {
      const post = {
        id: Math.floor(Math.random() * 10000),
        title: title.value,
        body: body.value,
        tags: tags.value
      }

      await fetch('http://localhost:3004/posts', {
        method: 'POST',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify(post)
      })

      router.push({ name: 'Home' })
    }

    return {
      title,
      body,
      tags,
      tag,
      router,
      handleKeyDown,
      handleSubmit,
    }
  }
}
</script>

<style scoped>
form {
  max-width: 480px;
  margin: 0 auto;
  text-align: left;
}
input,
textarea {
  display: block;
  margin: 10px 0;
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  border: 1px solid #eee;
}
textarea {
  height: 160px;
}
label {
  display: inline-block;
  margin-top: 30px;
  font-size: 20px;
  color: blueviolet;
  margin-bottom: 10px;
}
button {
  display: block;
  margin-top: 30px;
  background: blueviolet;
  color: white;
  border: none;
  padding: 8px 16px;
  font-size: 18px;
}
.pill {
  display: inline-block;
  margin: 10px 10px 0 0;
  color: white;
  background: blueviolet;
  padding: 8px;
  border-radius: 20px;
  font-size: 14px;
}
</style>