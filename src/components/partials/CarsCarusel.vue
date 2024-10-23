<script>
import CarCard from '../partials/CarCard.vue';
import axios from 'axios';
import { store } from '../../store';

export default {
    components: {
        CarCard,
    },
    data() {
        return {
            cars: [],
        };
    },
    created() {
        this.getCars();
    },
    methods: {
        getCars() {
            axios.get(`${store.baseUrl}/cars`).then((response) => {
                this.cars = response.data.results.data;
                this.cars = [...this.cars, ...this.cars];
            });
        },
        scrollLeft() {
            const container = this.$refs.carouselContainer;
            const card = container.querySelector('.car-card');
            const cardWidth = card.offsetWidth;
            const carouselContentStyle = window.getComputedStyle(
                container.querySelector('.carousel-content')
            );
            const gap = parseInt(carouselContentStyle.gap) || 0;
            const scrollAmount = cardWidth + gap;
            container.scrollBy({ left: -scrollAmount, behavior: 'smooth' });
        },
        scrollRight() {
            const container = this.$refs.carouselContainer;
            const card = container.querySelector('.car-card');
            const cardWidth = card.offsetWidth;
            const carouselContentStyle = window.getComputedStyle(
                container.querySelector('.carousel-content')
            );
            const gap = parseInt(carouselContentStyle.gap) || 0;
            const scrollAmount = cardWidth + gap;
            container.scrollBy({ left: scrollAmount, behavior: 'smooth' });
            if (container.scrollLeft + container.clientWidth >= container.scrollWidth) {
                setTimeout(() => {
                    container.scrollLeft = 0;
                }, 500);
            }
        },
    },
};
</script>

<template>
    <div class="container-fluid my-5">
        <h2>Auto più vendute</h2>
        <div class="car-carousel">
            <button @click="scrollLeft" class="scroll-btn left-btn">&#8249;</button>
            <div class="carousel-container" ref="carouselContainer">
                <div class="carousel-content" ref="carouselContent">
                    <CarCard
                        v-for="car in cars"
                        :key="car.id"
                        :car="car"
                        class="car-card"
                    />
                </div>
            </div>
            <button @click="scrollRight" class="scroll-btn right-btn">&#8250;</button>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .car-carousel {
        position: relative;
        display: flex;
        align-items: center;
    }

    .carousel-container {
        display: flex;
        overflow-x: auto;
        scroll-behavior: smooth;
        padding: 10px;
        gap: 15px;
        scrollbar-width: none;
    }

    .carousel-container::-webkit-scrollbar {
        display: none;
    }

    .carousel-content {
        display: flex;
        gap: 15px;
    }

    .car-card {
        flex: 0 0 auto;
        width: 300px;
    }

    .scroll-btn {
        background: rgba(0, 0, 0, 0.3);
        border: none;
        font-size: 2rem;
        cursor: pointer;
        padding: 10px;
        position: absolute;
        z-index: 100;
        top: 50%;
        transform: translateY(-50%);
        transition: background 0.3s ease;
        width: 50px;
        height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .left-btn {
        left: 10px;
    }

    .right-btn {
        right: 10px;
    }

    .scroll-btn:hover {
        background: rgba(0, 0, 0, 0.5);
    }
</style>
