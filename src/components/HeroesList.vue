<template>
    <div class="HeroesList">
        <h1>List</h1>
        <b-table striped hover :items="items" :fields="fields" caption-top>
        </b-table>
    </div>
</template>

<script>

export default {
    name: "HeroesList",
    data () {
        return {
            fields: ['name', 'score', 'id'],
            items: [
                { name: "Bob" , score: 151, id: 287921873},
                { name: "Nelson" , score: 700, id: 483948214},
                { name: "Charles" , score: 45, id: 49837124},
                { name: "Buck" , score: 77218 , id: 49837124},
            ]
        }
    },
    mounted () {
        
    }
}
</script>

<style scoped>

.HeroesList {
    width: 100%;
    height: 617px;
}
</style>

