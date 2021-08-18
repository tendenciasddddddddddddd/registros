<template>
    <div>

       
        <section class="section section section-shaped my-0 overflow-hidden">
            <div class="shape shape-style-1 bg-gradient-warning shape-skew">
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
            </div>
            <div class="container py-0">
                <div class="row row-grid align-items-center">
                    <div class="col-md-6 order-lg-2 ml-lg-auto">
                        <div class="position-relative pl-md-5">
                            <img src="img/ill/ill-2.svg" class="img-center img-fluid">
                        </div>
                    </div>
                    <div class="col-lg-6 order-lg-1">
                        <div class="d-flex px-3">
                            <div>
                                <icon name="ni ni-building" size="lg" class="bg-gradient-white" color="primary" shadow
                                      rounded></icon>
                            </div>
                            <div class="pl-4">
                                <h4 class="display-3 text-white">Felicitaciones</h4>
                                <p class="text-white">Gracias por brindarnos tu información, sera util para 
                                    los procesos academicos de la UNIDAD EDUCATIVA Monseñor Leonidas Proaño PCEI
                                </p>
                            </div>
                        </div>
                        <card shadow class="shadow-lg--hover mt-5">
                            <div class="d-flex px-3">
                                <div>
                                    <icon name="ni ni-satisfied" gradient="success" color="white" shadow
                                          rounded></icon>
                                </div>
                                <div class="pl-4">
                                    <h5 class="title text-success">Noticias </h5>
                                    <p>Estamos preparando un sistema informático basado en servicios que será de gran utilidad para tu formación académica, el cual tiene como objetivo integrar matriculas en línea, notas, asistencias y aulas virtuales. Gracias.</p>
                                   
                                </div>
                            </div>
                        </card>
                        <br>
                        <br>
                        <router-link to="/" type="button" class="btn btn-default">Regresar</router-link>
                    </div>
                </div>
            </div>
        </section>
      

    </div>
</template>

<script>
export default {
  name: "home",
  components: {}
};
</script>
