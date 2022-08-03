<script setup lang="ts">
import axios from 'axios'

const githubToken = import.meta.env.VITE_GITHUB_TOKEN
const name = ref('')
const pageNumber = ref(1)
const user = useUserStore()

async function search(name: string, page: number) {
  try {
    axios.get(`https://api.github.com/search/users?q=${name}&per_page=10&page=${page}`, {
      headers: {
        Authorization: `token ${githubToken}`,
      },
    })
      .then((response) => {
        user.setList(response.data)
      })
  }
  catch (error) {
    /* eslint-disable no-console */
    console.log(error)
    /* eslint-enable no-console */
  }
}

watch(name, (newValue) => {
  search(newValue, pageNumber.value)
})

watch(pageNumber, (newValue) => {
  search(name.value, newValue)
})

const { t } = useI18n()
</script>

<template>
  <div>
    <div text-4xl>
      <div animate-bounce-alt animate-count-infinite animate-duration-4s i-carbon-campsite inline-block />
    </div>
    <p>
      <a rel="noreferrer" href="https://github.com/antfu/vitesse" target="_blank">
        {{ t('search.search') }}
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
    >
    <label class="hidden" for="input">{{ t('intro.whats-your-name') }}</label>

    <div flex justify-center>
      <button v-if="pageNumber >= 2" @click="(pageNumber--)">
        back
      </button>
      <button
        v-if="!name"
        btn m-3 text-sm
        :disabled="!name"
      >
        {{ t('button.go') }}
      </button>
      <button
        v-if="name"
        btn m-3 text-sm
      >
        {{ t('button.woah') }}
      </button>
      <button v-if="name" @click="(pageNumber++)">
        next
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
