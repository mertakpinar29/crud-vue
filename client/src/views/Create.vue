<template>
  <PostForm :post="post" :submitForm="createPost" />
</template>

<script>
import PostForm from '../components/PostForm.vue'
import { reactive } from 'vue'
import { useRouter } from 'vue-router'
export default {
  components: {
    PostForm,
  },
  setup() {
    const API_URL = 'http://localhost:5000/posts'
    const router = useRouter()

    const post = reactive({
      title: '',
      content: '',
      creator: '',
    })

    async function createPost() {
      try {
        const response = await fetch(API_URL, {
          method: 'POST',
          headers: {
            'content-type': 'application/json',
          },
          body: JSON.stringify({
            title: post.title,
            content: post.content,
            creator: post.creator,
          }),
        })
        const json = await response.json()
        router.push({
          name: 'Home',
        })
      } catch (error) {
        console.log(error)
      }
    }
    return {
      post,
      createPost,
    }
  },
}
</script>

<style></style>
