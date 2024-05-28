<template>
    <h2>ИЗБРАННОЕ</h2>
    <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index" className="favsPars">
        <span>{{ el.from }}</span>
        <span>{{ el.to }}</span>
    </div>
</template>
  
<script>
    export default {
        props: {
            favs: {
                type: Array,
                required: true
            },
            getFromFavs: {
                type: Function,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>
