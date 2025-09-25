<script setup lang="ts">
const route = useRoute()

const slug = route.params.slug

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

const { data:article } = await useAsyncData<Article>(`artile-${slug}`, async () => {
    const collection = 
        await queryCollection('content')
        .path(`/${slug}`)
        .select('title', 'description', 'path', 'body', 'meta')
        .first()
    
    return {
        title: collection!.title,
        description: collection!.description,
        path: collection!.path,
        body: collection!.body,
        meta: {
            image: collection!.meta.image as string,
            tag: collection!.meta.tag as string[],
            date: collection!.meta.date as string
        }
    }
})
</script>
<template>
    <div class="bg-[url(/images/dot_saturn.png)] min-h-screen">
        <ArticleLayout
        v-if="article"
        :article="article"
        />
        <p v-else>記事が見つかりませんでした</p>
    </div>
</template>