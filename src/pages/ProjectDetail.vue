<template>
    <h1 v-if="project">{{ project.title }}</h1>
    <img :src="store.imgBasePath + project.image" :alt="project.title">
</template>

<script>
import axios from "axios";
import { store } from "../store";
    export default {
        name: 'ProjectDetail',
        data(){
            return {
                project: [],
                store,
            }
        },
        methods: {
            getProject(){
                // console.log(this.$route);
                axios.get(`${this.store.apiUrl}projects/${this.$route.params.slug}`).then((res) => {
                    if(res.data.results){
                        this.project = res.data.results;
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

</style>