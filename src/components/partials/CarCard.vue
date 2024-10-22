<script>
export default {
    name: 'CarCard',
    props: {
        car: Object
    }
}
</script>

<template>
    <div class="col-3" v-if="car">
        <div class="card-car h-100">
            <router-link class="text-reset text-decoration-none" :to="{ name: 'show_car', params: { slug: car.slug } }">
                <div class="img-card position-relative">
                    <img class="card-img-top img-fluid" :src="car.thumb">
                    <div :class="['badge-position', car.used ? 'used' : 'new']">
                        {{ car.used ? 'Usata' : 'Nuova' }}
                    </div>
                </div>
                <div class="card-body px-3 pt-2">
                    <h5 class="card-title">{{ car.brand.name }} {{ car.model }}</h5>
                    <div>{{ car.engine }}</div>
                    <div class="d-flex justify-content-between pt-1">
                        <div>{{ car.year }} - {{ car.km }} km</div>
                        <div class="fw-bold">€{{ car.price }}</div>
                    </div>
                </div>
            </router-link>
        </div>
    </div>
</template>


<style lang="scss" scoped>

    .card-car {
        display: block; 
        margin-bottom: 20px;
        line-height: 1.42857143;
        background-color: #ffffff98;
        border-radius: 2px;
        box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16),0 2px 10px 0 rgba(0,0,0,0.12); 
        transition: box-shadow .25s; 
    }
    .card-car:hover {
        box-shadow: 0 8px 17px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
    }
    .img-card {
        width: 100%;
        height:200px;
        display:block;
    }
    .img-card img{
        width: 100%;
        height: 200px;
        object-fit:cover; 
        transition: all .25s ease;
    }

    .card-title {
        margin-top:0px;
        font-weight: 700;
        font-size: 1.65em;
    }

    .badge-position {
        position: absolute;
        top: 10px; 
        right: 10px; 
        padding: 5px 10px; 
        text-transform: uppercase;
        border-radius: 5px;
    }
    
    .used {
        background-color: yellow;
    }
    
    .new {
        background-color: red;
        color: white;
    }

</style>