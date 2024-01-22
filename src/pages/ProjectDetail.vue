<template>
    <h2>ProjectDetail</h2>
    <h3>{{ this.project.title }}</h3>
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
                console.log(this.$route);
                axios.get(`${this.store.apiUrl}projects/${this.$route.params.slug}`).then((res) => {
                    this.project = res.data.results;
                    console.log(this.project);
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