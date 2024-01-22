<template>
    <main class="container">
        <h1 class="text-white text-center">Projects List</h1>
        <div class="row justify-content-between gap-lg-0 gap-3">
            <div class="col-12 col-lg-4 p-0" v-for="item in store.projects" :key="item.id">
                <AppCard :project="item" class="mx-2" />
            </div>
        </div>
        <div class="d-flex justify-content-end py-5">
            <div class="bg-danger-subtle p-2">
                <button class="btn btn-primary" @click="prevPage()"><i class="fa-solid fa-arrow-left"></i></button>
                <button class="btn btn-primary" @click="currentPage = n, getAllProjects()" :class="currentPage == n ? 'active' : '' " v-for="n in lastPage" :key="n">{{ n }}</button>
                <button class="btn btn-primary" @click="nextPage()"><i class="fa-solid fa-arrow-right"></i></button>
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
                currentPage: 1,
                lastPage: 0,
            }
        },
        methods: {
            getAllProjects(){
                axios.get(`${this.store.apiUrl}projects${this.store.urlPagination}${this.currentPage}`).then((res) => {
                    store.projects = res.data.results.data;
                    this.lastPage = res.data.results.last_page;
                    console.log(store.projects);
                }).catch((err) => {
                    console.log(err);
                })
            },
            nextPage(){
                if(this.currentPage < this.lastPage){
                    this.currentPage++;
                } else {
                    this.currentPage = 1;
                }
                this.getAllProjects();
            },
            prevPage(){
                this.currentPage--;
                if(this.currentPage == 0){
                    this.currentPage = this.lastPage;
                }
                this.getAllProjects();
            }
        },
        mounted(){
            this.getAllProjects();
        }
    }
</script>

<style lang="scss" scoped>

button {
    border-radius: 0!important;
}

</style>