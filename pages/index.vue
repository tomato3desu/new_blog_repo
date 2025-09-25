<script setup lang="ts">

const DEFAULT_IMAGE = 'images/default.jpg'

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

const { data:articles } = await useAsyncData<Article[]>('content', async () => {
    const collections = await queryCollection('content').select('title', 'description', 'path', 'meta').all()
    return collections.map(collection => ({
        title: collection.title,
        description: collection.description,
        path: collection.path,
        meta:{
            image: collection.meta.image as string ?? DEFAULT_IMAGE,
            tags: collection.meta.tags as string[],
            date: collection.meta.date as string
        }
    }))
})

//選択中のタグ
const selectedTag = ref<string | null>(null)

//記事をタグでフィルタリング
const filteredArticles = computed<Article[]>(() => {
    //articlesが空ならreturn
    if(!articles.value) return []

    let list: Article[] = []

    //selectedTagがnull(=すべてが選択されている)なら全部listに追加
    //selectedTagがあるならその値と一致するもののみlistに追加
    for(let doc of articles.value){
        if(selectedTag.value === null){
            list.push(doc)
        }else{
            if(doc.meta.tags.includes(selectedTag.value)){
                list.push(doc)
            }
        }
    }

    //記事を日付順にsort
    return list.sort(
        (a, b) => new Date(b.meta.date).getTime() - new Date(a.meta.date).getTime()
    )
})

//タグ一覧
const allTags = computed<string[]>(() => {
    let set = new Set<string>()

    if(articles.value === null){
        return []
    }

    for(let doc of articles.value){
        for(let tag of doc.meta.tags){
            set.add(tag)
        }
    }

    return Array.from(set)
})

</script>
<template>
    <div class="bg-[url(/images/dot_saturn.png)] min-h-screen">
        <div class="flex gap-4 p-4">
            <button
            class="px-3 py-1 rounded bg-gray-200"
            :class="{ 'bg-blue-400 text-white': selectedTag === null }"
            @click="selectedTag = null"
            >すべて</button>
            <button
            v-for="tag in allTags"
            :key="tag"
            class="px-3 py-1 rounded bg-gray-200"
            :class="{ 'bg-blue-400 text-white': selectedTag === tag }"
            @click="selectedTag = tag"
            >{{ tag }}</button>
        </div>


        <div class="p-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
            <CardLayout
            v-for="article in filteredArticles"
            :article="article"
            :key="article.path"
            />
        </div>
    </div>
</template>