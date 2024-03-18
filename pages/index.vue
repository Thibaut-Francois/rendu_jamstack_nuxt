<script setup lang="ts">

    const { find } = useStrapi()

    const { data, pending, error } = await useAsyncData('players', async () => {
        return await find('players', {
            populate: '*',
        })
    })
</script>

<template>
    <TheHeader />
    <h1>Hello world</h1>
    <About />
</template>

<style scoped></style>