<script setup lang="ts">
import axios from 'axios'

const props = defineProps<{ user: any; index: number }>()
const githubToken = import.meta.env.VITE_GITHUB_TOKEN

const router = useRouter()
const { t } = useI18n()
const isShowing = ref(false)
</script>

<template>
  <div flex justify-center flex-wrap>
    <img v-if="isShowing === index" animate-bounce-alt animate-count-infinite animate-duration-4s class="flex flex-shrink mx-4 w-20  align-middle" :src="props.user.avatar_url">
    <img v-else class="flex flex-shrink mx-4 w-20  align-middle" :src="props.user.avatar_url">
    <div class="flex flex-col flex-grow-2 justify-center">
      <p text-2xl class="text-left">
        <small>username: </small>{{ props.user.login }}
      </p>
      <p class="text-left">
        followers: {{ props.user.login }}
      </p>
    </div>
    <div justify-center class="flex flex-col flex-grow">
      <div flex class="justify-right">
        <a class="text-right" :href="props.user.html_url">
          View Profile
        </a>
        <a class="text-right" :href="props.user.html_url">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
          </svg>
        </a>
      </div>

      <div flex>
        <a class="text-right" :href="props.user.repos_url">
          View Repos
        </a>
        <a class="text-right" :href="props.user.repos_url">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
          </svg>
        </a>
      </div>
    </div>
  </div>
  <div flex flex-col justify-center bottom-5 right-0 left-0 text-center op30 fw300>
    <button
      v-if="!isShowing"
      @click="isShowing = !isShowing"
    >
      View Details
    </button>
    <button
      v-if="isShowing"
      @click="isShowing = !isShowing"
    >
      Hide Details
    </button>
  </div>
  <div v-if="isShowing">
    <MoreInfo :url="props.user.url" />
  </div>
</template>
