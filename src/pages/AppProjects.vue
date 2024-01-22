<template>
    <main class="container">
        <h1>Projects List</h1>
        <div class="row">
            <div class="col-12 col-md-4 col-lg-3" v-for="item in store.projects" :key="item.id">
                <AppCard :project="item" />
            </div>
        </div>
    </main>
</template>

<script>
import axios from "axios";
import { store } from "../store";
import AppCard from "../components/AppCard.vue";
    export default {
        name: 'AppProjects',
        components: {
            AppCard,
        },
        data(){
            return {
                store,
            }
        },
        methods: {
            getAllProjects(){
                axios.get(`${this.store.apiUrl}projects`).then((res) => {
                    store.projects = res.data.results.data;
                }).catch((err) => {
                    console.log(err);
                })
            }
        },
        mounted(){
            this.getAllProjects();
        }
    }
</script>

<style lang="scss" scoped>

</style>