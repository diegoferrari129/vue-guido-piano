<template>
    <footer class="footer">
        <div class="container-fluid px-5">
            <div class="row">
                <div class="col-md-3">
                    <h5>Società</h5>
                    <ul class="footer-links">
                        <li><a href="#">A proposito di GuidoPiano</a></li>
                        <li><a href="#">Stampa</a></li>
                        <li><a href="#">Condizioni generali</a></li>
                        <li><a href="#">Informazioni</a></li>
                        <li><a href="#">Privacy</a></li>
                    </ul>
                </div>
                <div class="col-md-3">
                    <h5>Servizi</h5>
                    <ul class="footer-links">
                        <li><a href="#">Contatti</a></li>
                        <li><a href="#">Marche e modelli</a></li>
                        <li><a href="#">Auto usate per regione</a></li>
                        <li><a href="#">Consigli</a></li>
                    </ul>
                </div>
                <div class="col-md-3">
                    <h5>Area rivenditori</h5>
                    <ul class="footer-links">
                        <li><a href="#">Servizi per i dealer</a></li>
                        <li><a href="#">Login</a></li>
                        <li><a href="#">Registrazione</a></li>
                        <li><a href="#">Contatti</a></li>
                    </ul>
                </div>
                <div class="col-md-3">
                <h5>Sempre con te</h5>
                <ul class="footer-links">
                    <li><a href="#"><i class="fas fa-mobile-alt"></i> GuidoPiano per iOS</a></li>
                    <li><a href="#"><i class="fas fa-mobile-alt"></i> GuidoPiano per Android</a></li>
                </ul>
                <div class="social-icons">
                    <a href="#" class="social-icon"><i class="fab fa-linkedin"></i></a>
                    <a href="#" class="social-icon"><i class="fab fa-instagram"></i></a>
                    <a href="#" class="social-icon"><i class="fab fa-facebook-f"></i></a>
                    <a href="#" class="social-icon"><i class="fab fa-youtube"></i></a>
                    <a href="#" class="social-icon"><i class="fab fa-tiktok"></i></a>
                </div>
                    <select class="country-selector">
                        <option value="italia">Italia</option>
                        <option value="usa">USA</option>
                        <option value="germany">Germania</option>
                    </select>
                </div>
            </div>
            <div class="footer-bottom">
                <p>&copy; 2024 GuidoPiano S.p.A. Tutti i diritti riservati. | P. IVA IT0000000000</p>
                <p>GuidoPiano fa parte della famiglia di soluzioni per il mercato automobilistico.</p>
            </div>
        </div>
    </footer>
</template>

<script>
    export default {};
</script>

<style lang="scss" scoped>
    .footer {
        background-color: #f8f9fa;
        padding: 40px 0;
        font-size: 14px;
        color: #333;
    }

    .footer h5 {
        font-weight: bold;
        margin-bottom: 20px;
    }

    .footer .footer-links {
        list-style: none;
        padding: 0;
    }

    .footer .footer-links li {
        margin-bottom: 10px;
    }

    .footer .footer-links a {
        text-decoration: none;
        color: #333;
    }

    .footer .footer-links a:hover {
        text-decoration: underline;
    }

    .footer .social-icons {
        margin-top: 20px;
    }

    .footer .social-icon {
        margin-right: 10px;
        color: #333;
        font-size: 18px;
    }

    .footer .social-icon:hover {
        color: #007bff;
    }

    .footer .country-selector {
        margin-top: 20px;
        padding: 5px;
        border-radius: 4px;
        border: 1px solid #ddd;
        width: 100%;
    }

    .footer-bottom {
        margin-top: 40px;
        border-top: 1px solid #ddd;
        padding-top: 20px;
        text-align: center;
        font-size: 12px;
    }

    .footer-bottom p {
        margin: 0;
    }

    .footer .fas,
    .footer .fab {
        margin-right: 5px;
    }
</style>