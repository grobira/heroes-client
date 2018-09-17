<template>
    <div class="HeroesList">
        <h1>List</h1>
        <b-table striped hover :items="items" :fields="fields" caption-top>
        </b-table>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "HeroesList",
    data () {
        return {
            fields: ['name', 'hp', 'status', 'class', 'breed'],
            items: []
        }
    },
    mounted () {
        axios
        .get("http://localhost:3001/heroes")
        .then(response => {
            this.items= this.listFilter(response.data);
        });
    },
    methods: {
        listFilter(data) {
            var list = [];
            data.map( element => {
                list.push({ name: element.firstname + " " + element.lastname, hp: Math.floor(element.hp), status: this.getStringStatus(element.status), class: element.class, breed: element.breed });
            });
            return list;
        },
        getStringStatus(status){
            var statusStr = "Str: " + Math.floor(status.str) + " Int: " + Math.floor(status.int) + " Dex: " + Math.floor(status.dex) + " Lck: " + Math.floor(status.lck);
            return statusStr;
        },
        updateList(){
            axios
            .get("http://localhost:3001/heroes")
            .then(response => {
                this.items= this.listFilter(response.data);
            });
        }
    }
}
</script>

<style scoped>

.HeroesList {
    width: 100%;
    height: 617px;
    overflow-y: auto;
}

::-webkit-scrollbar {
    width: 10px;
}

::-webkit-scrollbar-track {
    background: #f1f1f1; 
}

::-webkit-scrollbar-thumb {
    background: #888; 
}

::-webkit-scrollbar-thumb:hover {
    background: #555; 
}
</style>

