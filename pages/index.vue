<script setup lang="ts">

   const { find } = useStrapi()

   const { data: player, pending, error } = await useAsyncData('players', async () => {
       return await find('players', {
            populate: '*'
       })
   })

   const { data: tag} = await useAsyncData('tags', async () => {
       return await find('tags', {
            populate: '*'
       })
   })

    const filter =ref('')
</script>

<template>
    <h1>Hello World</h1>
    <select id="filter" v-model="filter">
        <option value="nofilter">All</option>
        <option v-for="oneTag in tag?.data" :key="oneTag.slug" :value="oneTag.name">{{ oneTag.name }}</option>
    </select>



    <section>
        <a :href="`/players/${onePlayer.slug}`" v-for="onePlayer in player?.data" :key="onePlayer.slug">{{ onePlayer.name }}</a>
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