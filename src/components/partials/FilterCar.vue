<script>
export default {
  props: {
    brands: {
      type: Array,
      required: true,
    },
    onFilter: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      searchQuery: '',
      selectedBrand: '',
      selectedYear: '',
      selectedPrice: '',
      selectedKm: '',
      selectedEngine: '',
      selectedHorsepower: '',
      years: Array.from({length: 31}, (_, i) => new Date().getFullYear() - i),
    };
  },
  methods: {
    applyFilters() {
      const filters = {
        search: this.searchQuery,
        brand: this.selectedBrand,
        year: this.selectedYear,
        price: this.selectedPrice,
        km: this.selectedKm,
        engine: this.selectedEngine,
        horsepower: this.selectedHorsepower,
      };
      this.onFilter(filters);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="row mb-4 pb-2 pt-4">
      <div class="col-12">
        <form class="search-bar d-flex justify-content-start align-items-end gap-2 py-4 flex-wrap" @submit.prevent="applyFilters">
          
          <div class="form-group flex-grow-1">
            <label for="search">Cerca auto:</label>
            <input
              type="text"
              id="search"
              class="form-control"
              v-model="searchQuery"
              placeholder="Cerca per marca o modello"
            />
          </div>
          
          <div class="form-group">
            <label for="year-filter">Anno:</label>
            <select id="year-filter" class="form-control" v-model="selectedYear">
              <option value="">Tutti gli anni</option>
              <option v-for="year in years" :key="year" :value="year">{{ year }}</option>
            </select>
          </div>

          <div class="form-group">
            <label for="price-filter">Prezzo:</label>
            <select id="price-filter" class="form-control" v-model="selectedPrice">
              <option value="">Tutti i prezzi</option>
              <option value="low">Meno di €50,000</option>
              <option value="medium">€50,000 - €150,000</option>
              <option value="high">Più di €150,000</option>
            </select>
          </div>

          <div class="form-group">
            <label for="km-filter">Chilometri:</label>
            <select id="km-filter" class="form-control" v-model="selectedKm">
              <option value="">Tutti i KM</option>
              <option value="low">Meno di 10,000 km</option>
              <option value="medium">10,000 - 50,000 km</option>
              <option value="high">Più di 50,000 km</option>
            </select>
          </div>

          <div class="form-group">
            <label for="engine-filter">Motore:</label>
            <select id="engine-filter" class="form-control" v-model="selectedEngine">
              <option value="">Tutti i motori</option>
              <option value="V6 Diesel">V6 Diesel</option>
              <option value="V6 Benzina">V6 Benzina</option>
              <option value="V8 Benzina">V8 Benzina</option>
              <option value="V10 Benzina">V10 Benzina</option>
              <option value="W12 Benzina">W12 Benzina</option>
              <option value="Elettrico">Elettrico</option>
            </select>
          </div>

          <div class="form-group">
            <label for="horsepower-filter">Cavalli:</label>
            <select id="horsepower-filter" class="form-control" v-model="selectedHorsepower">
              <option value="">Tutti i cavalli</option>
              <option value="low">Meno di 500</option>
              <option value="medium">500 - 700</option>
              <option value="high">Più di 700</option>
            </select>
          </div>

          <button type="submit" class="btn f-btn">Filtra</button>
        </form>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.search-bar {
  background-color: rgb(139, 128, 106);
  border-radius: 10px;
  padding: 20px;
  color: white;
}

.form-group {
  min-width: 150px;
}

.f-btn{
  background-color: #f8f9faa9;
}
</style>