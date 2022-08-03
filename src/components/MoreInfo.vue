<script setup lang="ts">
import axios from 'axios'

const props = defineProps<{ url: string }>()

const githubToken = import.meta.env.VITE_GITHUB_TOKEN
const router = useRouter()
const { t } = useI18n()
const userInfo = ref({})
const blog = ref('')
try {
  axios.get(props.url, {
    headers: {
      Authorization: `token ${githubToken}`,
    },
  })
    .then((response) => {
      userInfo.value = response.data
    })
}
catch (error) {
  /* eslint-disable no-console */
  console.log(error)
  /* eslint-enable no-console */
}
</script>

<template>
  <div flex flex-cols justify-around>
    <div>
      <h4 v-if="userInfo.name">
        <small>{{ t('details.name') }}: </small>{{ userInfo.name }}
      </h4>
      <h4 v-if="userInfo.location">
        <small>{{ t('details.location') }}: </small>{{ userInfo.location }}
      </h4>
      <h4 v-if="userInfo.email">
        <small>{{ t('details.email') }}: </small><a :href="`mailto:${userInfo.email}`">{{ userInfo.email }}</a>
      </h4>

      <h4 v-if="userInfo.created_at">
        <small>{{ t('details.created') }}: </small>{{ userInfo.created_at }}
      </h4>
    </div>
    <div>
      <h4 v-if="userInfo.public_repos">
        <small>{{ t('details.repos') }}: </small>{{ userInfo.public_repos }}
      </h4>
      <h4 v-if="userInfo.public_gists">
        <small>{{ t('details.gists') }}: </small>{{ userInfo.public_gists }}
      </h4>
      <h4 v-if="userInfo.followers">
        <small>{{ t('details.followers') }}: </small>{{ userInfo.followers }}
      </h4>
      <h4 v-if="userInfo.blog">
        <small>{{ t('details.blog') }}: </small><a :href="userInfo.blog">{{ userInfo.blog }}</a>
      </h4>
      <h4 v-if="userInfo.updated_at">
        <small>{{ t('details.updated') }}: </small>{{ userInfo.updated_at }}
      </h4>
    </div>
  </div>
</template>
