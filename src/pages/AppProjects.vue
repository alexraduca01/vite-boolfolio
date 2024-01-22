<template>
    <div>
        <h1>Projects List</h1>
        <ul>
            <li class="mb-2" v-for="item in store.projects" :key="item.id">
                <router-link :to="{ name: 'project', params: { slug: item.slug } }" class="btn btn-primary" >{{ item.title }}</router-link>
            </li>
            
        </ul>
    </div>
</template>

<script>
import axios from "axios";
import { store } from "../store";
    export default {
        name: 'AppProjects',
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