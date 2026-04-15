<template>
    <section class="row">
        <div id="carouselExampleIndicators" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-indicators">
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active"
                    aria-current="true" aria-label="Slide 1"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"
                    aria-label="Slide 2"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2"
                    aria-label="Slide 3"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="3"
                    aria-label="Slide 4"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="4"
                    aria-label="Slide 5"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="5"
                    aria-label="Slide 6"></button>
            </div>

            <div class="carousel-inner">
                <div class="carousel-item active">
                    <img src="/images/Carrusel1c.webp" class="d-block w-100" alt="Slide 1">
                    <div class="carousel-caption d-none d-md-block">
                        <h2>Creemos en la conservación y el desarrollo</h2>
                        <br>
                        <a href="/services" class="cbotoncar">Mas información</a>
                        <br>
                        <br>
                    </div>
                </div>
                <div class="carousel-item">
                    <img src="/images/Carrusel2c.webp" class="d-block w-100" alt="Slide 2">
                    <div class="carousel-caption d-none d-md-block">
                        <h2>Impulsamos sistemas agroforestales</h2>
                        <br>
                        <a href="/services" class="cbotoncar">Mas información</a>
                        <br>
                        <br>
                    </div>
                </div>
                <div class="carousel-item">
                    <img src="/images/Carrusel3c.webp" class="d-block w-100 c-image" alt="Slide 3">
                    <div class="carousel-caption d-none d-md-block">
                        <h2>Apoyamos la producción sostenible</h2>
                        <br>
                        <a href="/services" class="cbotoncar">Mas información</a>
                        <br>
                        <br>
                    </div>
                </div>
                <div class="carousel-item">
                    <img src="/images/Carrusel4c.webp" class="d-block w-100" alt="Slide 4">
                    <div class="carousel-caption d-none d-md-block">
                        <h2>Producimos material de calidad</h2>
                        <br>
                        <a href="/services" class="cbotoncar">Mas información</a>
                        <br>
                        <br>
                    </div>
                </div>
                <div class="carousel-item">
                    <img src="/images/Carrusel5c.webp" class="d-block w-100" alt="Slide 5">
                    <div class="carousel-caption d-none d-md-block">
                        <h2>Acompañamos sueños en crecimiento</h2>
                        <br>
                        <a href="/services" class="cbotoncar">Mas información</a>
                        <br>
                        <br>
                    </div>
                </div>
                <div class="carousel-item">
                    <img src="/images/Carrusel6c.webp" class="d-block w-100" alt="Slide 6">
                    <div class="carousel-caption d-none d-md-block">
                        <h2>Le acompañamos en el proceso del cambio</h2>
                        <br>
                        <a href="/services" class="cbotoncar">Mas información</a>
                        <br>
                        <br>
                    </div>
                </div>
            </div>

            <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleIndicators"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleIndicators"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
        </div>
    </section>
</template>

<style scoped>

.row {
    margin-top: 0 !important;
}
/* ============================================================
   CAROUSEL CONTENEDOR
   ============================================================ */
.carousel {
    width: 100%;
    padding: 0;
}

/* ============================================================
   CAROUSEL ITEM E IMÁGENES
   ============================================================ */
.carousel-item {
    background-color: #777;
    overflow: hidden;
}

.carousel-item img {
    height: 100%;
    object-fit: cover;
    width: 100%;
}

/* Ajuste de posición para la imagen del slide 3 en móvil */
.c-image {
    object-position: center center;
}

/* ============================================================
   BOTÓN CTA DEL CAROUSEL
   ============================================================ */
.cbotoncar {
    color: #000;
    background-color: #ffb209;
    font-size: 1.75rem;
    border-radius: 10px;
    padding: 10px 25px;
    font-weight: 800;
}

/* ============================================================
   MEDIA QUERY — MÓVIL
   ============================================================ */
@media screen and (max-width: 775px) {
    .c-image {
        object-position: 70% 75%;
    }
    .carousel-item {
        height: 210px;
    }
}
</style>
