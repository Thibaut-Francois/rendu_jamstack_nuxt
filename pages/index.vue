<script setup lang="ts">

   const { find } = useStrapi()

   const { data, pending, error } = await useAsyncData('players', async () => {
       return await find('players', {
            populate: '*'
       }).then(res => res.data)
   })

</script>

<template>
    <h1>Hello World</h1>
    <section>
        <a :href="`/players/${player.slug}`" v-for="player in data" :key="player.slug">{{ player.name }}</a>
    </section>
</template>

<style scoped>
    h1 {
        color: red;
    }
    section {
        display: flex;
        flex-direction: column;
    }
    a {
        margin: 10px 0;
    }

    a:hover {
        text-decoration: underline;
    }
</style>