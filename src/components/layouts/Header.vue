<script>
export default {
    props: {
        menu: Array
    }
}
</script>

<template>
    <header class="navbar navbar-expand-lg navbar-dark">
      <div class="container-fluid">
        <router-link class="navbar-brand" :to="{ name: 'home' }">
          <span class="logo-text"><span class="logo-highlight">Guido</span>Piano</span>
        </router-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse ms-3" id="navbarNav">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="me-4" v-for="(item, index) in menu" :key="index">
                <router-link class="text-reset text-decoration-none" :to="{ name: item.name }">{{item.label}}</router-link>
            </li>
          </ul>
        </div>
      </div>
    </header>
  </template>

<style lang="scss">
header {
    background-color: #333;
    height: 60px;
    line-height: 60px;

    .navbar-brand {
        display: flex;
        align-items: center;
        font-size: 1.5rem;
        color: #fff;

        .logo-highlight {
            background-color: #ffc107;
            color: #000;
            padding: 0 5px;
            border-radius: 4px;
            margin-right: 5px;
        }
    }

    .navbar-nav .nav-link {
        color: #e0e0e0;
        margin-right: 15px;
        transition: color 0.3s ease;
    }

    .navbar-nav .nav-link.active {
        color: #ffc107;
    }

    .navbar-nav .nav-link:hover {
        color: #ffc107;
    }

    .btn-outline-light {
        border-color: #ffc107;
        color: #ffc107;
        transition: background-color 0.3s ease, color 0.3s ease;
    }

    .btn-outline-light:hover {
        background-color: #ffc107;
        color: #000;
    }

    .navbar-toggler {
        border: none;
    }

    .d-flex img {
        width: 16px;
        height: auto;
    }

    .navbar-collapse {
        justify-content: space-between;
    }

    .dropdown-menu {
        background-color: #333;
        border: none;
    }

    .dropdown-item {
        color: #fff;
        transition: background-color 0.3s ease, color 0.3s ease;
    }

    .dropdown-item:hover {
        background-color: #000;
        color: #fff;
    }

    @media (max-width: 768px) {
        .navbar-nav {
            text-align: center;
        }

        .navbar-nav .nav-item {
            margin-bottom: 10px;
        }

        .navbar-nav .nav-link {
            margin-right: 0;
        }
    }
}

</style>