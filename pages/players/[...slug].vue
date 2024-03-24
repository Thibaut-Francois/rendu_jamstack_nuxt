<script lang="ts" setup>
const { findOne } = useStrapi4()
const route = useRoute()

const {data: player, pending, error} = await useAsyncData('player', async () => findOne(`players/${route.params.slug}`))

// const { data: player, pending, error } = await useAsyncData('player', async () => {
//        return await find('player', {
//             populate: '*'
//        })
//    })


</script>

<template>
    <div class="info">
        <p>pseudo: {{ player?.data.name }}</p>
        <p>real name: {{ player?.data.family_name }}</p>
        <p>role: {{ player?.data.tags[0].name }}</p>
        <p>ranking: {{ player?.data.ranking }}</p>
    </div>
    
</template>

<style>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .info{
        margin: 10px;
        font-size: 20px;
    }
</style>