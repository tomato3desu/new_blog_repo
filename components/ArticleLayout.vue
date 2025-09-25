<script setup lang="ts">
interface Article {
  title: string
  description: string
  path: string
  body: any
  meta: {
    image: string
    tag: string[]
    date: string
  }
}

const { article } = defineProps<{
    article: Article
}>()
</script>
<template>
    <div class="prose mx-auto bg-white rounded-xl p-2 min-h-screen">
        <h1 class="text-3xl font-bold">{{ article?.title }}</h1>
        <p class="text-gray-600 mt-2">{{ article?.description }}</p>
        <img
        v-if="article?.meta.image"
        :src="article.meta.image"
        class="mt-4 rounded-lg shadow"
        />
        <p class="mt-6 text-sm text-gray-500">投稿日: {{ article?.meta.date }}</p>
        <ContentRenderer :value="article?.body" class="prose"/>
    </div>
</template>