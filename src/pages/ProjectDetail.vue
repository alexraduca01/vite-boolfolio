<template>
    <div v-if="project" class="container bg-dark h-100">
        <h1 class="text-white text-center">{{ project.title }}</h1>
        <div class="text-white">
            <p>{{ project.body }}</p>
            <p>{{ categoryName }}</p>
            <!-- <p>{{ project.category.name }}</p> -->
            <ul class="d-flex list-unstyled gap-3">
                <li v-for="item in project.technologies">
                    <img :src="item.image" class="tech-img" :alt="item.title">
                </li>
            </ul>
        </div>
        <img class="img-fluid" :src="store.imgBasePath + project.image" :alt="project.title">
    </div>
</template>

<script>
import axios from "axios";
import { store } from "../store";
    export default {
        name: 'ProjectDetail',
        data(){
            return {
                project: [],
                categoryName: '',
                store,
            }
        },
        methods: {
            getProject(){
                // console.log(this.$route);
                axios.get(`${this.store.apiUrl}projects/${this.$route.params.slug}`).then((res) => {
                    if(res.data.results){
                        this.project = res.data.results;
                        this.categoryName = this.project.category.name
                        console.log(this.project);
                    } else {
                        this.$router.push({ name: 'not-found' });
                    }
                    
                    // console.log(this.project);
                })
            }
        },
        mounted(){
            this.getProject();
        }
    }
</script>

<style lang="scss" scoped>

.tech-img {
    width: 40px;
    height: 40px;
}
</style>