<template>
  <section class="section section-shaped section-lg my-0">
    <div class="shape shape-style-1 bg-gradient-default">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>
    <div class="container pt-lg-md">
      <div class="row justify-content-center">
        <div class="col-lg-10">
          <card
            type="secondary"
            shadow
            header-classes="bg-white pb-5"
            body-classes="px-lg-5 py-lg-5"
            class="border-0"
          >
            <template>
              <div class="text-center text-muted mb-4">
                <h4>Queremos saber mas de ti</h4>
                <h3>{{id}}</h3>
              </div>
              <form @submit.prevent="save" role="form">
                <div class="row">
                  <div class="col-6">
                    <input
                      alternative
                      v-model="model.telefonofijo"
                      class="form-control mb-3"
                      type="number"
                      placeholder="Teléfono Fijo"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                   />
                    
                    <textarea
                     v-model="model.calles"
                      alternative
                      class="form-control mb-3"
                      placeholder="Calles"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />

                    <textarea
                      alternative
                      v-model="model.referencia"
                      class="form-control mb-3"
                      placeholder="Referencia de su vivienda"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                    <input
                      alternative
                      class="form-control mb-3"
                      type="number"
                       v-model="model.codigo"
                      placeholder="Codigo de Luz"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                    <input
                      alternative
                      class="form-control mb-3"
                      type="text"
                       v-model="model.nombrec"
                      placeholder="Nombres de Representante o tutor"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                    <input
                      alternative
                      class="form-control mb-3"
                      type="number"
                       v-model="model.numeric"
                      placeholder="Numero de Representante o tutor"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                  
                    <v-select
                      
                      :options="parentesco"
                      label="nombre"
                      item-value="nombre"
                      v-model="model.parentesc"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                   <br>
                    <input
                      alternative
                      class="form-control mb-3"
                      type="text"
                       v-model="model.tiposangre"
                      placeholder="Tipo de Sangre"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                  </div>
                  <div class="col-6">
                          <label>Fecha Nacimiento</label>
                      <input
                      @change="onChange($event)"
                      alternative
                      class="form-control mb-3"
                      type="date"
                       v-model="model.nacimineto"
                      
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                       <input
                      alternative
                      class="form-control mb-3"
                      type="number"
                       v-model="model.edad"
                      placeholder="Edad"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                      readonly
                    />
                    <label>Centro de Atencion</label>
                    <v-select
                      :options="centroAtenci"
                      label="nombre"
                      v-model="model.centroAtencio"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                    <label>Estado del Estudiante</label>
                   
                    <v-select
                      
                      :options="estadoEstudiante"
                      label="nombre"
                      v-model="model.estadoEstudiant"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>

                    <label>Tipo de Documnto</label>
                   
                    <v-select
                      
                      :options="tipoDocumnte"
                      label="nombre"
                      v-model="model.tipoDocumnt"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                    <label>Estado Civil</label>
                   
                    <v-select
                     
                      :options="estadoCivil"
                      label="nombre"
                      item-value="nombre"
                      v-model="model.estadoCivi"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                    <label>Operador</label>
                    <v-select
                      :options="operador"
                      label="nombre"
                      item-value="nombre"
                      v-model="model.operado"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                     <label>Si tiene discapacidad ingrese su carnet(Opcional)</label>
                    <input
                      alternative
                      class="form-control mb-3"
                      type="number"
                       v-model="model.discapacidad"
                      placeholder="123..."
                      addon-left-icon="ni ni-zoom-split-in"
                    />
                  </div>
                </div>

                <div class="text-center">
                    <br>
                    <base-button v-if="ifLoad" size="my-4" type="primary" disabled>Enviando...</base-button>
                  <button v-else  type="submit" class="btn btn-info"
                    >Guardar Formulario</button
                  >
                </div>
              </form>
            </template>
          </card>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import axios from "axios";
export default {
  name: "Register",
  data() {
    return {
      centroAtenci: [
        {
          value: "0",
          nombre: "Miercoles Tulcán",
        },
        {
          value: "1",
          nombre: "Sábado Tulcán",
        },
        {
          value: "2",
          nombre: "Nocturno Tulcán",
        },
        {
          value: "3",
          nombre: "Huaca",
        },
        {
          value: "4",
          nombre: "San Gabriel",
        },
        {
          value: "5",
          nombre: "El Ángel",
        },
      ],
        estadoEstudiante: [
        {
          value: "0",
          nombre: "Estudiante Recien desea Ingresar",
        },
        {
          value: "1",
          nombre: "Estudiante ya existente",
        }, 
      ],
        tipoDocumnte: [
        {
          value: "0",
          nombre: "Cédula",
        },
        {
          value: "1",
          nombre: "Pasaporte",
        }, 
         {
          value: "3",
          nombre: "Visa",
        },
        {
          value: "4",
          nombre: "Carner de Refugiado",
        },
         {
          value: "5",
          nombre: "Otro",
        },
      ],
      estadoCivil: [
        {
          value: "0",
          nombre: "Solter@",
        },
        {
          value: "1",
          nombre: "Casad@",
        }, 
         {
          value: "3",
          nombre: "Divorciad@",
        },
        {
          value: "4",
          nombre: "Viud@",
        },
         {
          value: "5",
          nombre: "Union Libre",
        },
      ],
       operador: [
        {
          value: "0",
          nombre: "Claro",
        },
        {
          value: "1",
          nombre: "Movistar",
        }, 
         {
          value: "3",
          nombre: "CNT",
        },
        {
          value: "4",
          nombre: "Tuenti",
        },
         {
          value: "5",
          nombre: "Otros",
        },
      ],
        parentesco: [
        {
          value: "0",
          nombre: "Padre - Madre",
        },
        {
          value: "1",
          nombre: "Esposo - Esposa",
        }, 
         {
          value: "3",
          nombre: "Hermano - Hermana",
        },
        {
          value: "4",
          nombre: "Abuelo - Abuela",
        },
         {
          value: "5",
          nombre: "Otros",
        },
      ],

      model: {
           telefonofijo: null,
           calles: null,
           referencia: null,
           codigo: null,
           numeric: null,
           nombrec: null,
           edad: null,
            centroAtencio: null ,
            estadoEstudiant: null,
            tipoDocumnt: null, 
            estadoCivi: null, 
            tiposangre: null, 
            operado: null, 
            carnet: null,
             parentesc: null,
              discapacidad: null,  
              detalles: null,
              nacimineto: null,
        //-----------VARIABLES DEL MODELO A GUARDAR
        
      },
    
      ifLoad: null,
      id: '',
    };
  },
  methods: {
      get(){
            if(this.$route.params.id){
              this.id= this.$route.params.id;
            }else{
                this.$router.push("/");
            }
      },



     save() {
      //-----------BOTTON DE GUADAR TIENE VALIDAR Y SI EL ID ES NULL ENTONCES GUARDA
     this.ifLoad = true;
          if(this.model.centroAtencio==null||
          this.model.estadoEstudiant==null||
          this.model.tipoDocumnt==null||
          this.model.estadoCivi==null||
          this.model.operado==null||
          this.model.parentesc==null ) {
            alert("LLENE TODOS LOS CAMPOS");
            this.ifLoad = false;
            return;
          }
          this.model.centroAtencio = this.model.centroAtencio.nombre;
          this.model.estadoEstudiant = this.model.estadoEstudiant.nombre;
          this.model.tipoDocumnt = this.model.tipoDocumnt.nombre;
          this.model.estadoCivi = this.model.estadoCivi.nombre;
          this.model.operado = this.model.operado.nombre;
          this.model.parentesc = this.model.parentesc.nombre;
          this.model.detalles = this.id;
         console.log(this.model)
          //
              axios.post("https://pcei-app.herokuapp.com/api/userdelles", this.model).then((result) => {
                
                this.$router.push("/landing");
                this.ifLoad = false;
               })
               .catch((error) => {
              //-----------EN CASO DE TENER DUPLICADO LOS DOCUMENTOS EL SERVIDOR LANZARA LA EXEPCION
              this.ifLoad = false;
              if (error.response) {
                if (error.response.status == 400) {
                  alert("Error: " + error.response.data.message)
                }
                if (error.response.status == 500) {
                  alert('No se puede procesar los datos');
                }
              } else if (error.request) {
                alert("duplicado 2");
              } else {
                console.log("Error", error.message);
              }
            });
   
    },
      onChange(event) {
      let hoy = new Date();
      let fechaNacimiento = new Date(event.target.value);
      let edad = hoy.getFullYear() - fechaNacimiento.getFullYear();
      let diferenciaMeses = hoy.getMonth() - fechaNacimiento.getMonth();
      if (
        diferenciaMeses < 0 ||
        (diferenciaMeses === 0 && hoy.getDate() < fechaNacimiento.getDate())
      ) {
        edad--;
      }
      this.model.edad = edad;
    },
  },
  created() {
      this.get();
  },
};
</script>
<style></style>
