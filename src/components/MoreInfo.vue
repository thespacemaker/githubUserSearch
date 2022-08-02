<script setup lang="ts">
import axios from 'axios'

const props = defineProps<{ url: string }>()

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
  <div flex flex-cols justify-around>
    <div>
      <h4 v-if="userInfo.name">
        <small>Name: </small>{{ userInfo.name }}
      </h4>
      <h4 v-if="userInfo.location">
        <small>Location: </small>{{ userInfo.location }}
      </h4>
      <h4 v-if="userInfo.email">
        <small>email: </small><a :href="`mailto:${userInfo.email}`">{{ userInfo.email }}</a>
      </h4>

      <h4 v-if="userInfo.created_at">
        <small>Created Profile: </small>{{ userInfo.created_at }}
      </h4>
    </div>
    <div>
      <h4 v-if="userInfo.public_repos">
        <small>Number of Public Repos: </small>{{ userInfo.public_repos }}
      </h4>
      <h4 v-if="userInfo.public_gists">
        <small>Number of public_gists: </small>{{ userInfo.public_gists }}
      </h4>
      <h4 v-if="userInfo.followers">
        <small>followers: </small>{{ userInfo.followers }}
      </h4>
      <h4 v-if="userInfo.blog">
        <small>blog: </small><a :href="userInfo.blog">{{ userInfo.blog }}</a>
      </h4>
      <h4 v-if="userInfo.updated_at">
        <small>Last Updated: </small>{{ userInfo.updated_at }}
      </h4>
    </div>
  </div>
</template>
