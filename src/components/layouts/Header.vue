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
            <a class="navbar-brand" href="/">
                <span class="logo-text">Guido</span><span class="logo-highlight">Piano</span>
            </a>

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

                <div class="d-flex align-items-center">
                    <a class="btn btn-outline-light me-3" href="#">
                        <i class="fas fa-user"></i> Account
                    </a>
                    <a class="btn btn-outline-light" href="#">
                        <i class="fas fa-shopping-cart"></i> Carrello
                    </a>
                </div>
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

/* Style for the account and cart buttons */
.btn-outline-light {
    color: #f8f9fa; 
    border: 1px solid #f8f9fa;
    transition: all 0.3s;
    font-family: 'Roboto', sans-serif;
}

.btn-outline-light:hover {
    background-color: #ffc107;
    border-color: #ffc107;
    color: #000;
}

.d-flex {
    margin-left: auto; /* Ensures buttons stay to the right */
}

/* Icon size adjustment */
.fas {
    margin-right: 5px;
}
</style>
