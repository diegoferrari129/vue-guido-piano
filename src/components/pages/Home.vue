<script>
    import CarsCarusel from '../partials/CarsCarusel.vue';
    import Info from '../partials/Info.vue';
    import Carusel from '../partials/Carusel.vue';
  

    export default {
        components: {
            CarsCarusel,
            Info,
            Carusel,

        },
    };
</script>

<template>
    <img src="/image-1.png" alt="Jumbotron"class="img-fluid"/>
    <div class="container">
        <div class="jumbotron-section">
            <img src="/jumbotron.webp" alt="Jumbotron" class="jumbotron-image" />
            <div class="jumbotron-overlay">
                <h1 class="jumbotron-title">Benvenuto nel nostro sito di automobili</h1>
                <p class="jumbotron-text">Trova la tua prossima auto o vendi quella che hai con facilità!</p>
            </div>
        </div>
        <Info/>
        <Carusel/>
        <CarsCarusel/>
    </div>

</template>


<style lang="scss" scoped>
    .container-fluid {
        padding: 0;
    }

    .jumbotron-section {
        position: relative;
        width: 100%;
        height: 400px;
        overflow: hidden;
        margin-bottom: 30px;
    }

    .jumbotron-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .jumbotron-overlay {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.4);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: white;
        padding: 20px;
        text-align: center;
    }

    .jumbotron-title {
        font-size: 36px;
        font-weight: bold;
        margin-bottom: 10px;
    }

    .jumbotron-text {
        font-size: 18px;
    }
</style>