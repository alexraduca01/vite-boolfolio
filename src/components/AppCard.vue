<template>
    <div class="card">
        <img :src="store.imgBasePath + project.image" class="card-img-top img-fluid" :alt="project.title">
        <router-link :to="{ name: 'project', params: { slug: project.slug } }" class="btn btn-primary" >{{ project.title }}</router-link>
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