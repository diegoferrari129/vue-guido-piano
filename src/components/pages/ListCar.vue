<script>
import CarCard from '../partials/CarCard.vue';
import { store } from '../../store';
import axios from 'axios';

export default {
  components: {
      CarCard,
  },
  data() {
      return {
          store,
          cars: [],
          last_page: null,
          current_page: null,
      }
  },
  created() {
      this.getCars();
  },
  methods: {
      getCars() {
          axios.get(`${store.baseUrl}/cars`).then((response) => {
              this.cars = response.data.results.data;
              this.last_page = response.data.results.last_page;
              this.current_page = response.data.results.current_page;
          });
      },
      goToPage(page) {
          axios.get(`${store.baseUrl}/cars`, { params: { page: page } }).then((response) => {
              this.cars = response.data.results.data;
              this.current_page = response.data.results.current_page;
          });
      },
  }
}
</script>

<template>
  <div class="container-fluid">
      <div class="row">
          <div class="col-12">
              <div class="text-center py-5">
                  <h1>Cars</h1>
              </div>
          </div>
      </div>
      <div class="row gy-3">
        <CarCard v-for="car in cars" :key="car.id" :car="car" />
      </div>
      <div class="row">
          <div class="col-12">
              <nav aria-label="Page navigation example" class="d-flex justify-content-center py-3">
                  <ul class="pagination">
                      <li class="page-item">
                          <a class="page-link" :class="current_page == 1 ? 'disabled' : ''" href="#" @click.prevent="goToPage(current_page - 1)">Previous</a>
                      </li>
                      <li class="page-item" v-for="index in last_page" :key="index">
                          <a class="page-link" href="#" @click.prevent="goToPage(index)">{{ index }}</a>
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


<style lang="scss"></style>