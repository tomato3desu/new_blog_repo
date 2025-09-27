<script setup lang="ts">
const router = useRouter()
const goToTop = () => {
    router.push("/")
}
</script>
<template>
    <div class="border-b-4 shadow border-gray-300 flex h-20 items-center justify-between px-4">
        <p class="text-4xl font-bit text-rose-500" @click="goToTop">tomato</p>
        <div class="flex gap-6">
            <a href="https://x.com/QzItUJ08S246159" target="_blank" rel="noopener noreferrer" aria-label="X (Twitter)"> 
                <font-awesome-icon icon="fa-brands fa-x-twitter" class="h-8"/>
            </a>
            <a href="https://github.com/tomato3desu" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
                <font-awesome-icon icon="fa-brands fa-github" class="h-8"/>
            </a>
        </div>
    </div>
</template>