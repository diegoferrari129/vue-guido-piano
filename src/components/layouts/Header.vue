<script>
export default {
    props: {
        menu: Array
    }
}
</script>

<template>
    <header class="navbar navbar-expand-lg custom-header">
        <div class="container-fluid">
            <router-link class="navbar-brand" :to="{ name: 'home' }">
                <span class="logo-text">Guido</span><span class="logo-highlight">Piano</span>
            </router-link>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse ms-3" id="navbarNav">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item" v-for="(item, index) in menu" :key="index">
                        <router-link class="nav-link" :to="{ name: item.name }">{{ item.label }}</router-link>
                    </li>
                </ul>
            </div>
        </div>
    </header>
</template>

<style lang="scss" scoped>
.custom-header {
    background-color: rgb(139, 128, 106) !important;
}

.logo-text, .logo-highlight {
    font-size: 1.5rem; 
    font-weight: bold;
}

.logo-text {
    color: #ffffff; 
}

.logo-highlight {
    color: #ff0000; 
}

.navbar-nav .nav-link {
    color: #f8f9fa; 
    transition: color 0.3s;
    margin-right: 20px; 
    font-family: 'Roboto', sans-serif; 
}

.navbar-nav .nav-link:hover {
    color: #ffc107; 
}

</style>