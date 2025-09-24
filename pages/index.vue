<script setup lang="ts">

const { data:articles } = await useAsyncData('content', () => {
    return queryCollection('content').select('title', 'description', 'path', 'meta').all()
})


</script>
<template>
    <div>
        <p class="text-4xl text-sky-200 font-bit">tomato</p>
        <ul>
            <li v-for="article in articles" :key="article.path">
                <h2>{{ article.title }}</h2>
                <p>{{ article.description }}</p>
                <small>{{ article.meta.date }}</small>
            </li>
        </ul>
    </div>
</template>