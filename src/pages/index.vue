<script setup lang="ts">
import axios from 'axios'

const githubToken = import.meta.env.VITE_GITHUB_TOKEN
const user = useUserStore()
const name = ref('')
const namefromStore = $ref(user.savedName)

watch(name, (newValue) => {
  axios.get(`https://api.github.com/search/users?q=${newValue}`, {
    headers: {
      Authorization: `token ${githubToken}`,
    },
  })
    .then((response) => {
      user.setList(response.data)
      console.log(user.userList)
    })
})

const router = useRouter()
const go = () => {
  if (name)
    router.push(`/hi/${encodeURIComponent(name)}`)
}

const { t } = useI18n()
</script>

<template>
  <div>
    <div text-4xl>
      <div i-carbon-campsite inline-block />
    </div>
    <p>
      <a rel="noreferrer" href="https://github.com/antfu/vitesse" target="_blank">
        Github Search
      </a>
    </p>
    <p>
      <em text-sm opacity-75>{{ t('intro.desc') }}</em>
    </p>

    <div py-4 />

    <input
      id="input"
      v-model="name"
      :placeholder="t('intro.whats-your-name')"
      :aria-label="t('intro.whats-your-name')"
      type="text"
      autocomplete="false"
      p="x4 y2"
      w="250px"
      text="center"
      bg="transparent"
      border="~ rounded gray-200 dark:gray-700"
      outline="none active:none"
      @keydown.enter="go"
    >
    <label class="hidden" for="input">{{ t('intro.whats-your-name') }}</label>

    <div>
      <button
        btn m-3 text-sm
        :disabled="!name"
        @click="go"
      >
        {{ t('button.go') }}
      </button>
    </div>
    <div v-if="user.userList">
      <div v-for="(listItem, index) in user.userList.items" :key="listItem.id" class="pa-4 ma-4 border-cyan rounded-xl justify-left border-2 md:w-200 sm:w-100 mx-auto">
        <UserResults :user="listItem" :index="index" />
      </div>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
