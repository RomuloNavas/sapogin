<script setup lang="ts">
import { useUserStore } from '~/stores/user'

const props = defineProps<{ name: string }>()
const router = useRouter()
const user = useUserStore()

watchEffect(() => {
  user.setNewName(props.name)
})
</script>

<template>
  <div>
    <div text-4xl>
      <div i-carbon-pedestrian inline-block />
      <div i-carbon-close inline-block />
    </div>
    <p> Hi <span text-indigo-500 uppercase>{{ props.name }}</span></p>
    <template v-if="user.otherNames.length">
      <p text-sm mt-4>
        <span opacity-90>Also known as:</span>
        <ul>
          <li v-for="otherName in user.otherNames" :key="otherName" opacity-50 hover:underline>
            <router-link :to="`/hi/${otherName}`" replace>
              <!-- If you use replace, then when you will go back, you will not go to the dynamic name, you will go to "/"  -->
              {{ otherName }}
            </router-link>
          </li>
        </ul>
      </p>
    </template>

    <div>
      <button
        btn-white mt-4
        @click="router.back()"
      >
        Go back
      </button>
    </div>
  </div>
</template>
