<template>
    <form @submit.prevent="submitForm()">
        <div class="mb-3 text-white">
            <label for="name" class="form-label">Name</label>
            <input type="text" class="form-control" id="name" aria-describedby="nameHelp" v-model="name">
            <div id="nameHelp" class="form-text text-white">Insert your name</div>
        </div>
        <div class="mb-3 text-white">
            <label for="email" class="form-label">Email address</label>
            <input type="email" class="form-control" id="email" aria-describedby="emailHelp" v-model="email">
            <div id="emailHelp" class="form-text text-white">We'll never share your email with anyone else.</div>
        </div>
        <div class="mb-3 text-white">
            <label for="address" class="form-label">Your address</label>
            <input type="text" class="form-control" id="address" aria-describedby="addressHelp" v-model="address">
            <div id="addressHelp" class="form-text text-white">Insert your address</div>
        </div>
        <div class="mb-3 text-white">
            <label for="message" class="form-label">Your message</label>
            <textarea id="message" class="form-control" aria-describedby="message" cols="30" rows="10" v-model="message"></textarea>
            <div id="messageHelp" class="form-text text-white">Insert your message</div>
        </div>
        <button type="submit" class="btn btn-primary me-3">Submit</button>
        <button type="reset" class="btn btn-danger">Reset</button>
    </form>
</template>

<script>
import { store } from '../store';
import axios from 'axios';
    export default {
        name: 'ContactForm',
        data(){
            return {
                store,
                name: '',
                email: '',
                address: '',
                message: '',
            }
        },
        methods: {
            submitForm(){
                const formData = {
                    name: this.name,
                    email: this.email,
                    address: this.address,
                    message: this.message
                };
                axios.post(this.store.apiUrl + 'contacts', formData).then((res) => {
                    console.log(res.data);
                    this.name = '';
                    this.email = '';
                    this.address = '';
                    this.message = '';
                }).catch((err) => {
                    console.log('error', err);
                })
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>