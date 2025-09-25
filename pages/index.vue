<script setup lang="ts">

const DEFAULT_IMAGE = 'images/default.jpg'

interface Article {
    title: string
    description: string
    path: string
    meta: {
        image?: string
        tag?: string[]
        date: string
    }
}

const { data:articles } = await useAsyncData<Article[]>('content', async () => {
    const collections = await queryCollection('content').select('title', 'description', 'path', 'meta').all()
    return collections.map(collection => ({
        title: collection.title,
        description: collection.description,
        path: collection.path,
        meta:{
            image: (collection.meta.image as string | undefined) ?? DEFAULT_IMAGE,
            tag: collection.meta.tag as string[] | undefined,
            date: collection.meta.date as string
        }
    }))
})


</script>
<template>
    <div class="bg-[url(/images/dot_saturn.png)] min-h-screen">
        <div class="p-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
            <CardLayout
            v-for="article in articles"
            :article="article"
            :key="article.path"
            />
        </div>
    </div>
</template>