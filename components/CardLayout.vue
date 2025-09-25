<script setup lang="ts">
interface Article {
  title: string
  description: string
  path: string
  meta: {
    image: string
    tags: string[]
    date: string
  }
}

const { article } = defineProps<{
  article: Article
}>()

const router = useRouter()

const goToArticle = () => {
    router.push(article.path)
}
</script>
<template>
    <NuxtLink class="bg-white rounded-2xl shadow p-4 hover:shadow-lg transition h-100" @click="goToArticle">
        <img
        v-if="article.meta.image"
        :src="article.meta.image"
        alt=""
        class="w-full h-40 object-cover rounded-xl mb-4"
        />
        <p class="text-xl font-semibold text-blue-600">{{ article.title }}</p>
        <p class="text-gray-600 mt-2 break-words">
        {{ article.description }}
        </p>
        <small class="text-sm mt-2 text-gray-600">{{ article.meta.date }}</small>
        <div class="flex gap-3">
            <small 
            v-for="tag in article.meta.tags"
            class="text-sm text-sky-400">#{{ tag }}</small>
        </div>
    </NuxtLink>
</template>