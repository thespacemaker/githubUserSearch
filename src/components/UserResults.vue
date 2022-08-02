<script setup lang="ts">
const props = defineProps<{ user: any }>()
const router = useRouter()
const { t } = useI18n()
</script>

<template>
  <div flex justify-center flex-wrap>
    <img class="flex flex-shrink mx-4 w-20  align-middle" :src="props.user.avatar_url">
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
</template>
