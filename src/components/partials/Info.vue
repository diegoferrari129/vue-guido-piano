<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-6 d-flex">
                <div class="advice-card">
                    <img src="/left-info.webp" alt="Left Info Image" class="card-image" />
                    <div class="card-overlay">
                        <span class="badge">CONSIGLI</span>
                        <h2 class="card-title">Acquista la tua auto in sicurezza con i consigli dei nostri esperti!</h2>
                        <a href="#" class="card-link">Informati qui →</a>
                    </div>
                </div>
            </div>
        
            <div class="col-md-6 d-flex">
                <div class="advice-card">
                    <img src="/right-info.webp" alt="Right Info Image" class="card-image" />
                    <div class="card-overlay">
                        <span class="badge">CONSIGLI</span>
                        <h2 class="card-title">Dai valore al tuo usato. Con il giusto prezzo. Calcola quanto vale la tua auto!</h2>
                        <a href="#" class="card-link">Valuta gratis →</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {};
</script>

<style lang="scss" scoped>
    .container-fluid {
        padding: 2rem 0;
    }

    .row {
        display: flex;
    }

    .advice-card {
        position: relative;
        border-radius: 8px;
        overflow: hidden;
        margin-bottom: 20px;
        display: flex;
        flex-direction: column;
        height: 100%; 
        min-height: 300px; /* Ensure cards are of equal height */
        flex-grow: 1;
    }

    .card-image {
        width: 100%;
        height: 100%; /* Cover the full card space */
        object-fit: cover; /* Ensures the image is proportionally resized */
        flex-shrink: 0;
    }

    .card-overlay {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.4);
        color: white;
        padding: 20px;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
    }

    .card-overlay .badge {
        position: absolute;
        top: 10px;
        left: 10px;
        background: black;
        padding: 5px 10px;
        font-size: 12px;
        text-transform: uppercase;
        border-radius: 4px;
        z-index: 1;
    }

    .card-title {
        font-size: 20px;
        font-weight: bold;
        margin-bottom: 10px;
    }

    .card-link {
        color: white;
        font-weight: bold;
        text-decoration: none;
    }

    .card-link:hover {
        text-decoration: underline;
    }
</style>