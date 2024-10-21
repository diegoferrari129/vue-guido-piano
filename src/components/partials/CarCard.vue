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
        <div class="card h-100">
            <router-link class="text-reset text-decoration-none" :to="{ name: 'show_car', params: { slug: car.slug } }">
                <div class="card_img">
                    <img class="card-img-top img-fluid" :src="car.image != null ? `http://127.0.0.1:8000/storage/${car.image}` : 'https://placehold.co/600x400?text=Hello+World'">
                </div>
                <div class="card-body">
                    <div class="d-flex justify-content-between">
                        <div>
                            <h5>{{ car.brand.name }} {{ car.model }}</h5>
                            <div>{{ car.engine }}</div>
                        </div>

                        <div>
                            <div class="text-end">
                                {{ car.used ? 'Usata' : 'Nuova' }}
                            </div>
                            <div>{{ car.year }} {{ car.km }} km</div>
                        </div>
                    </div>

                    <div class="card-footer d-flex justify-content-center bg-dark mt-2">
                        <span class="text-warning fw-bold">€{{ car.price }}</span>
                    </div>
                </div>
            </router-link>
        </div>
    </div>
</template>


<style lang="scss" scoped>



</style>