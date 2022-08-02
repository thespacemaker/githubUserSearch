<script setup lang="ts">
import axios from 'axios'

const props = defineProps<{ url: string; userDetails: any }>()

const githubToken = import.meta.env.VITE_GITHUB_TOKEN
const router = useRouter()
const { t } = useI18n()
const userInfo = ref({})
const blog = ref('')

axios.get(props.url, {
  headers: {
    Authorization: `token ${githubToken}`,
  },
})
  .then((response) => {
    userInfo.value = response.data
  })
</script>

<template>
  <div flex flex-cols>
    <div flex justify-between>
      <h4><small>blog: </small>{{ userInfo.blog }}</h4>
      <h4><small>blog: </small>{{ userInfo.blog }}</h4>
      <h4><small>blog: </small>{{ userInfo.blog }}</h4>
      <h4><small>blog: </small>{{ userInfo.blog }}</h4>
    </div>
  </div>
</template>
