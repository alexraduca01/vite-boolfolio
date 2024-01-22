<template>
    <div class="card">
        <div class="card-header">
            <img :src="store.imgBasePath + project.image" class="card-img-top img-fluid" :alt="project.title">
        </div>
        <div class="card-body text-center">
            <router-link :to="{ name: 'project', params: { slug: project.slug } }" class="btn btn-primary" >View More</router-link>
        </div>
    </div>
</template>

<script>
import { store } from "../store";
    export default {
        name: 'AppCard',
        props: ['project'],
        data(){
            return {
                store,
            }
        }
    }
</script>

<style lang="scss" scoped>



</style>