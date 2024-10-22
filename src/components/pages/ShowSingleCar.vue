<script>
import { store } from '../../store.js';
import axios from 'axios';

export default {
    data() {
        return {
            store,
            car: null,
            success: false
        }
    },
    created() {
        this.getCar();
    },
    methods: {
        getCar() {
            this.success = false;
            axios.get(`${store.baseUrl}/cars/${this.$route.params.slug}`).then((response) => {
                if (response.data.success) {
                    this.car = response.data.results;
                    this.success = true;
                } else {
                    this.$router.push({ name: 'not_found' });
                }
            });
        }
    }
}
</script>

<template>
    <div v-if="!success">
        Loading...
    </div>
    <div v-else class="container">
        <div class="row">
            <div class="col-4">
                <div class="my-5">
                    img
                </div>
            </div>
            <div class="col-4">
                <div class="my-5">
                   <h2>{{ car.brand.name }}</h2>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang=""></style>