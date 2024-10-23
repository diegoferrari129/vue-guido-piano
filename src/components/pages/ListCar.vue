<script>
  import CarCard from '../partials/CarCard.vue';
  import FilterCar from '../partials/FilterCar.vue';
  import { store } from '../../store';
  import axios from 'axios';

  export default {
    components: {
      CarCard,
      FilterCar,
    },

    data() {
      return {
        store,
        cars: [],
        filteredCars: [],
        last_page: null,
        current_page: null,
        brands: [],
      }
    },

    created() {
      this.getCars();
      this.getBrands();
    },

    methods: {
      getCars() {
        axios.get(`${store.baseUrl}/cars`).then((response) => {

          this.cars = response.data.results.data;
          this.filteredCars = this.cars; // Inizializza le auto filtrate
          this.last_page = response.data.results.last_page;
          this.current_page = response.data.results.current_page;
        });
      },

      getBrands() {
        axios.get(`${store.baseUrl}/brands`).then((response) => {
          this.brands = response.data;
        });
      },

      goToPage(page) {
        axios.get(`${store.baseUrl}/cars`, { params: { page: page } }).then((response) => {

          this.cars = response.data.results.data;
          this.filteredCars = this.cars; // Resetta il filtro
          this.current_page = response.data.results.current_page;
        });
      },

      applyFilters(filters) {
        this.filteredCars = this.cars.filter(car => {

          const matchesSearch = filters.search ? (car.brand.name.toLowerCase().includes(filters.search.toLowerCase()) || car.model.toLowerCase().includes(filters.search.toLowerCase())) : true;
          const matchesCondition = filters.condition ? (filters.condition === 'new' ? !car.used : car.used) : true; // Modifica qui
          const matchesBrand = filters.brand ? car.brand.id === filters.brand : true;
          const matchesYear = filters.year ? car.year === filters.year : true;
          const matchesPrice = this.filterByPrice(car.price, filters.price);
          const matchesKm = this.filterByKm(car.km, filters.km);
          const matchesEngine = filters.engine ? car.engine === filters.engine : true;
          const matchesHorsepower = this.filterByHorsepower(car.horsepower, filters.horsepower);

          return matchesSearch && matchesCondition && matchesBrand && matchesYear && matchesPrice && matchesKm && matchesEngine && matchesHorsepower;
        });
      },

      filterByPrice(price, filter) {
        if (filter === 'low') return price < 50000;
        if (filter === 'medium') return price >= 50000 && price <= 150000;
        if (filter === 'high') return price > 150000;

        return true;
      },
      
      filterByKm(km, filter) {
        if (filter === 'low') return km < 10000;
        if (filter === 'medium') return km >= 10000 && km <= 50000;
        if (filter === 'high') return km > 50000;

        return true;
      },

      filterByHorsepower(horsepower, filter) {
        if (filter === 'low') return horsepower < 500;
        if (filter === 'medium') return horsepower >= 500 && horsepower <= 700;
        if (filter === 'high') return horsepower > 700;
        return true;
        
      }
    }
  }
</script>

<template>
  <div class="container-fluid">
    <!-- Barra di ricerca e filtri -->
    <FilterCar :brands="brands" :onFilter="applyFilters" />

    <div class="row gy-4">
      <CarCard v-for="car in filteredCars" :key="car.id" :car="car" />
    </div>

    <div class="row">
      <div class="col-12">
        <nav aria-label="Page navigation example" class="d-flex justify-content-center py-4 mt-2">
          <ul class="pagination">
            <li class="page-item">
              <a class="page-link" :class="current_page == 1 ? 'disabled' : ''" href="#" @click.prevent="goToPage(current_page - 1)">Previous</a>
            </li>
            <li class="page-item" v-for="index in last_page" :key="index">
              <a class="page-link" :class="{ active: index === current_page }" href="#" @click.prevent="goToPage(index)">{{ index }}</a>
            </li>
            <li class="page-item">
              <a class="page-link" :class="current_page == last_page ? 'disabled' : ''" href="#" @click.prevent="goToPage(current_page + 1)">Next</a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .pagination {
    background-color: #ffffff98;
    border-radius: 5px; 
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.16);
    padding: 5px; 
  }

  .page-item {
    margin: 0 5px; 
  }

  .page-link {
    padding: 5px 15px;
    border-radius: 5px; 
    color: #333; 
    text-decoration: none; 
    transition: background-color 0.3s, color 0.3s;  
  }

  .page-link:hover {
    background-color: rgba(0, 0, 0, 0.1);
  }

  .page-link.active {
    background-color: rgb(139, 128, 106);
    color: white; 
  }

  .page-link.disabled {
    color: #aaa; 
    pointer-events: none; 
  }
</style>