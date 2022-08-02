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
        username: <small>{{ props.user.login }}</small>
      </p>
      <p class="text-left">
        followers: {{ props.user.login }}
      </p>
    </div>
    <div class="flex flex-col justify-center text-right">
      <a class="text-right" :href="props.user.url">
        View Profile
      </a>
      <p class="text-right">
        followers: {{ props.user.login }}
      </p>
    </div>
    <div justify-center class="flex flex-col flex-grow">
      <p class="text-right">
        followers: {{ props.user.followers }}
      </p>
      <p class="text-right">
        followers: {{ props.user.following }}
      </p>
    </div>
  </div>
  <div flex flex-col justify-center bottom-5 right-0 left-0 text-center op30 fw300>
    <button
      @click="isShowing = true"
    >
      View Details
    </button>
  </div>
  <div v-if="isShowing">
    <MoreInfo :url="props.user.url" />
  </div>
</template>
