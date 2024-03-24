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

    const filter =ref('nofilter')
    const search =ref('')
    
</script>

<template>
    <section v-if="pending">Loading...</section>
    <h1>League of Legends Pro Players</h1>

    <select id="filter" v-model="filter" aria-label="label for the select">
        <option value="nofilter">All</option>
        <option v-for="oneTag in tag?.data" :key="oneTag.slug" :value="oneTag.name">{{ oneTag.name }}</option>
    </select>

    <input type="text" v-model="search" placeholder="Search for a player">

    <div class="playerBox">
        <section v-for="onePlayer in player?.data" >
            <section class="allPlayers" v-if="filter === 'nofilter' || onePlayer.tags.some(tag => tag.name == filter) ">
                <section v-if="onePlayer.name.toLowerCase().startsWith(search.toLowerCase()) == true">
                    <a class="playerName" :href="`/players/${onePlayer.slug}`" :key="onePlayer.slug">
                    <p>{{ onePlayer.name }}</p>
                    <img :src="`${onePlayer.Images.formats.thumbnail.url}`">
                </a>
                </section>
            </section>
        </section>
    </div>

</template>

<style scoped>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    h1 {
        color: red;
    }
    a {
        margin: 10px 0;
    }
    
    a:hover {
        text-decoration: underline;
    }
    
    img {
        width: 100px;
    }
    
    .allPlayers {
        display: flex;
        flex-direction: column;
    }
    .playerBox {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
    .playerName{
        text-decoration: none;
        margin: 10px;
    }
</style>