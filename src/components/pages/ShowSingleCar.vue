<script>
import { store } from '../../store.js';
import axios from 'axios';

export default {
    data() {
        return {
            store,
            car: null,
            optionals: null,
            success: false,

            // SELEZIONA, DESELEZIONA UN'OPTIONAL
            selectedOptionals: [],

            // MESSAGGIO DI POP-UP PER L'AGGIUNTA O LA RIMOZIONE DEGLI OPTIONAL NEL CARRELLO 
            notification: {
                visible: false,
                message: '',
            }
        }
    },

    created() {
        this.getCar();
        this.getOptional();
    },

    computed: {
        // SOMMA DEL PREZZO AUTO + OPTIONALS
        totalPrice() {
            if (!this.car) return null;

            const optionalTotal = this.selectedOptionals.reduce((total, optional) => total + Number(optional.price), 0);

            return (Number(this.car.price) + optionalTotal).toFixed(2);
        }
    },
    methods: {
        // FORMATO DEL PREZZO
        formatPrice(value) {

            return new Intl.NumberFormat('it-IT', {

                style: 'decimal',
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            }).format(value);

        },
        
        // API CARS
        getCar() {
            this.success = false;

            axios.get(`${store.baseUrl}/cars/${this.$route.params.slug}`).then((response) => {

                if (response.data.success) {
                    this.car = response.data.results;
                    this.success = true;

                } else {
                    this.$router.push({ name: 'not_found' });
                }
            });
        },

        // API OPTIONALS
        getOptional() {
            this.success = false;

            axios.get(`${store.baseUrl}/optionals`).then((response) => {

                if (response.data.success) {
                    this.optionals = response.data.results;
                    this.success = true;

                } else {
                    this.$router.push({ name: 'not_found' });
                }
            });
        },

        // SELEZIONA, DESELEZIONA UN'OPTIONAL
        toggleOptional(optional) {

            const index = this.selectedOptionals.indexOf(optional);

            if (index > -1) {
                this.selectedOptionals.splice(index, 1);
                this.showNotification(`${optional.name} rimosso dal carrello.`);

            } else {
                this.selectedOptionals.push(optional);
                this.showNotification(`${optional.name} aggiunto al carrello.`);
            }
        },
        
        // MESSAGGIO DI POP-UP CON TIMEOUT PER L'AGGIUNTA O LA RIMOZIONE DEGLI OPTIONAL NEL CARRELLO 
        showNotification(message) {

            this.notification.message = message;
            this.notification.visible = true;

            setTimeout(() => {
                this.notification.visible = false;
            }, 5000);
        }
    }
};
</script>


<template>
    <!-- MESSAGGIO DI POP-UP PER L'AGGIUNTA O LA RIMOZIONE DEGLI OPTIONAL NEL CARRELLO -->
    <div v-if="notification.visible" class="notification">
        {{ notification.message }}
    </div>

    <!-- INIZIO DELLA PAGINA -->
    <div class="container-fluid">
        <div class="row">

            <!-- NOME E MODELLO DELL'AUTO -->
            <div class="col-12">
                <div class="car-header d-flex align-items-center justify-content-between bg-dark text-warning p-4">
                    <h1>{{ car.brand.name }} {{ car.model }}</h1>
                    
                    <!-- BOTTONE PER TORNARE ALLA LISTA DELLE AUTO -->
                    <a href="" class="btn btn-warning">Torna indietro</a>
                </div>
            </div>
        </div>

        <!-- INIZIO INFORMAZIONI SULL'AUTO -->
        <div class="row mt-4">
            
            <!-- IMMAGINE DELL'AUTO-->
            <div class="col-10">
                <img :src="car.thumb" class="img-fluid show-img shadow-lg">
            </div>

            <!-- CARDS DEI DETTAGLI DELL'AUTO -->
            <div class="col-2">
                <div class="row gy-2">
                    
                    <!-- USATA O NUOVA -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-check-circle text-warning"></i>
                            </div>

                            <div class="card-body">
                                <div><strong>{{ car.used ? 'Usata' : 'Nuova' }}</strong></div>
                            </div>
                        </div>

                    </div>
                    
                    <!-- COLORE -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-palette text-warning"></i>
                            </div>

                            <div class="card-body">
                                <div>Colore</div>
                                <div><strong>{{ car.color }}</strong></div>
                            </div>
                        </div>

                    </div>
                    
                    <!-- MOTORE -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-cogs text-warning"></i>
                            </div>

                            <div class="card-body">
                                <div>Motore</div>
                                <div><strong>{{ car.engine }}</strong></div>
                            </div>
                        </div>

                    </div>
                    
                    <!-- CAVALLI -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-horse text-warning"></i>
                            </div>

                            <div class="card-body">
                                <div>Cavalli</div>
                                <div><strong>{{ car.horsepower }}</strong></div>
                            </div>
                        </div>

                    </div>
                    
                    <!-- CHILOMETRAGGIO -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-road text-warning"></i>
                            </div>
                            
                            <div class="card-body">
                                <div>Chilometraggio</div>
                                <div><strong>{{ car.km }} km</strong></div>
                            </div>
                        </div>

                    </div>
                    
                    <!-- ANNO -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-calendar-alt text-warning"></i>
                            </div>
                            <div class="card-body">
                                <div>Anno</div>
                                <div><strong>{{ car.year }}</strong></div>
                            </div>
                        </div>
                        
                    </div>

                    <!-- PREZZO BASE -->
                    <div class="col-12">

                        <div class="card-car-info h-100">
                            <div>
                                <i class="fas fa-euro-sign text-warning"></i>
                            </div>

                            <div class="card-body">
                                <div>Prezzo Base</div>
                                <div><strong>€{{ car.price }}</strong></div>
                            </div>
                        </div>

                    </div>
                    
                </div>
            </div>

        </div>
        <!-- FINE INFORMAZIONI SULL'AUTO -->
        <hr>
        <!-- INIZIO SEZIONE OPTIONALS -->
        <div class="row mt-4">

            <!-- SOTTOTITOLO -->
            <div class="col-12">
                <h2 class="fw-bold pt-3 pb-2">Optional Disponibili per: {{ car.brand.name }} {{ car.model }}</h2>
            </div>
            
            <div class="col-12">
                <div class="row gy-4">

                    <!-- CICLO OPTIONALS -->
                    <div class="col-2" v-for="optional in optionals" :key="optional.id">

                        <!-- CARDS PER GLI OPTIONAL CON TOGGLE PER SELEZIONE, DESELEZIONE GLI OPTIONAL-->
                        <div class="card-car h-100 d-flex flex-column" @click="toggleOptional(optional)" :class="{'selected': selectedOptionals.includes(optional)}">

                            <!-- IMMAGINE OPTIONAL -->
                            <div class="img-card flex-grow-0">
                                <img class="card-img-top img-fluid" :src="optional.thumb" alt="Optional Image">
                            </div>

                            <!-- NOME E DESCRIZIONE OPTIONAL -->
                            <div class="card-body px-3 pt-2 flex-grow-1 d-flex flex-column">
                                <h3 class="card-title">{{ optional.name }}</h3>

                                <div class="card-text">
                                    <div class="pt-1">{{ optional.description }}</div>
                                </div>

                                <!-- PREZZO OPTIONAL, CON METODO PER IL FORMATO -->
                                <div class="text-end mt-auto mb-2">
                                    <div>Aggiungi con un costo di 
                                        <div><strong>€ {{ formatPrice(optional.price) }}</strong></div>
                                    </div>
                                </div>
                            </div>
                            
                        </div>

                    </div>

                </div>
            </div>
           
        </div>
        <!-- FINE CARDS OPTIONAL -->

        <!-- MOSTRO LA SOMMA FINALE -->
        <div class="row mt-4">
            <div class="col-12">
                
                <div class="card-car-info h-100">
                    <div class="card-body text-center">
                        <h3>Prezzo Totale</h3>
                        <div><strong>€ {{ formatPrice(totalPrice) }}</strong></div>
                    </div>
                </div>

            </div>
        </div>
    </div>
  </template>
  
  <style lang="scss">

    // IMMAGINE AUTO
    .show-img {
        width: 100%;
        height: 700px !important;
        object-fit: cover;
    }
    
    // CARDS DETTAGLI DELL'AUTO
    .card-car-info {
        display: flex;
        align-items: center;
        background-color: #f9f9f9;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 8px;
        text-align: center;
      
        i {
          font-size: 2rem;
        }
    }

    // CARDS OPTIONAL
    .card-car {
        display: block; 
        margin-bottom: 20px;
        line-height: 1.42857143;
        background-color: #ffffff98;
        border-radius: 2px;
        box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16),0 2px 10px 0 rgba(0,0,0,0.12); 
        transition: box-shadow .25s; 
    }
    
    // EFFETTO HOVER CARD OPTIONAL
    .card-car:hover {
        box-shadow: 0 8px 17px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
    }

    // IMMAGINE CARD OPTIONAL
    .img-card {
        width: 100%;
        height:200px;
        display:block;

        img{
            width: 100%;
            height: 200px;
            object-fit:cover; 
            transition: all .25s ease;
        }
    }

    // TITOLO CARD OPTIONAL
    .card-title {
        margin-top:0px;
        font-weight: 700;
        font-size: 1.65em;
    }

    // EFFETTO CARD OPTIONAL SELEZZIONATA
    .card-car.selected {
        border: 2px solid #f39c12;
    }

    // STILE POP-UP
    .notification {
        position: fixed;
        top: 0; 
        left: 0; 
        right: 0; 
        background-color: rgba(0, 123, 255, 0.8); 
        color: white;
        padding: 10px 0; 
        text-align: center; 
        transition: opacity 0.5s;
        z-index: 1000;
        opacity: 0;
        animation: slideDown 0.5s forwards;
    }

    // ANIMAZIONE POP UP
    @keyframes slideDown {
        from {
            transform: translateY(-100%);
            opacity: 1;
        }
        to {
            transform: translateY(0);
            opacity: 1;
        }
    }
    
  </style>