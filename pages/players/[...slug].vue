<script lang="ts" setup>
const { findOne } = useStrapi4()
const route = useRoute()

const {data: player, pending} = useAsyncData('player', () => findOne(`players/${route.params.slug}`))


</script>

<template>
    <h1>OUI</h1>
    <pre>{{ player?.data }}</pre>
</template>