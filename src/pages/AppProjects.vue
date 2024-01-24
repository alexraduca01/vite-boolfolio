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
        <div>
            <select @change="getFilteredProjects()" v-model="selected">
                <option value="">All</option>
                <option :value="item.name" v-for="item in store.categories"> {{ item.name }} </option>
            </select>
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
                selected: '',
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
            getAllCategories(){
                axios.get(`${this.store.apiUrl}categories`).then((res) => {
                    store.categories = res.data.results;
                    for(let i = 0; i < store.categories.length; i++){
                        this.filter.push(store.categories[i].name);
                    }
                    console.log(this.filter);
                    console.log(store.categories);
                }).catch((err) => {
                    console.log(err);
                })
            },
            getFilteredProjects(){
                axios.get(`${this.store.apiUrl}categories/projects${this.store.urlCategory}${this.selected}`).then((res) => {
                    store.projects = res.data.results;
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
        created(){
            this.getAllProjects();
            this.getAllCategories();
            // this.getFilteredProjects();
        }
    }
</script>

<style lang="scss" scoped>

button {
    border-radius: 0!important;
}

</style>