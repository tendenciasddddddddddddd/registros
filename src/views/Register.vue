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
          <router-link to="/" type="button" class="btn btn-default">Regresar</router-link>
            <template>
              <div class="text-center text-muted mb-4">
                <small>Ingrese la información</small>
              </div>
              <form @submit.prevent="save" role="form">
                <div class="row">
                  <div class="col-6">
                    <input
                      alternative
                       @change="__validarCedula($event)"
                      v-model="model.cedula"
                      class="form-control mb-3"
                      type="number"
                      placeholder="Cedula"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                   />
                    <p style="font-size: 12px" class="text-xs text-primary">{{mensaje}}</p>
                    <input
                     v-model="model.nombres"
                      alternative
                      class="form-control mb-3"
                      placeholder="Nombres"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />

                    <input
                      alternative
                      v-model="model.apellidos"
                      class="form-control mb-3"
                      placeholder="Apellidos"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                    <input
                      alternative
                      class="form-control mb-3"
                      type="number"
                       v-model="model.telefono"
                      placeholder="Numero Celular"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                    <input
                      alternative
                      class="form-control mb-3"
                      type="email"
                       v-model="model.email"
                      placeholder="Correo Electronico"
                      addon-left-icon="ni ni-zoom-split-in"
                      required
                    />
                  </div>
                  <div class="col-6">
                    <label>Genero</label>
                    <v-select
                      :options="sexos"
                      label="nombre"
                      v-model="model.sexo"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                    <label>Etnia</label>
                    <p v-if="isetnia">Espere un momento..</p>
                    <v-select
                      v-else
                      :options="result"
                      label="nombre"
                      v-model="model.fketnia"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>

                    <label>Nacionalidad</label>
                    <p v-if="isetnia1">Espere un momento..</p>
                    <v-select
                      v-else
                      :options="result1"
                      label="nombre"
                      v-model="model.fknacionalidad"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                    <label>Parroquia <a href="https://wa.me/+593969721145">(Click Si no encuentras tu parroquia)</a></label>
                    <p v-if="isetnia2">Espere un momento..</p>
                    <v-select
                      v-else
                      :options="result2"
                      label="nombre"
                      item-value="nombre"
                      v-model="model.fkparroquia"
                      required
                    >
                      <template #option="{ nombre }">
                        <h6 style="margin: 0">{{ nombre }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                    <label>Modalidad</label>
                    <v-select
                      :options="modalidad"
                      label="name"
                      item-value="nombre"
                      v-model="model.modalidad"
                      required
                    >
                      <template #option="{ name }">
                        <h6 style="margin: 0">{{ name }}</h6>
                      </template>
                      <template #no-options="{ }">
                        Lo siento, no hay opciones de coincidencia.
                      </template>
                    </v-select>
                  </div>
                </div>

                <div class="text-center">
                    <br>
                    <base-button v-if="ifLoad" size="my-4" type="primary" disabled>Enviando...</base-button>
                  <button v-else  type="submit" class="btn btn-info"
                    >Crear Cuenta</button
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
      sexos: [
        {
          value: "0",
          nombre: "Masculino",
        },
        {
          value: "1",
          nombre: "Femenino",
        },
        {
          value: "2",
          nombre: "Otros",
        },
        {
          value: "3",
          nombre: "No conforme",
        },
      ],
      checked: null,
      radio: {
        radio1: "radio1",
        radio2: "radio3",
      },
      model: {
        //-----------VARIABLES DEL MODELO A GUARDAR
        _id: null,
        username: null,
        email: null,
        password: null,
        nombres: null,
        apellidos: null,
        cedula: null,
        foto:
          "https://firebasestorage.googleapis.com/v0/b/back-ends.appspot.com/o/perfiles%2Fprofile.jpg?alt=media&token=bf6ad3bb-84a5-442a-8ac0-4a906e3ec1bd",
        typo: "ESTS",
        status: null,
        telefono: null,
        updatedAt: null,
        role: null,
        ////////////////////////////////
        sexo: null,
        fketnia: null,
        fknacionalidad: null,
        fkparroquia: null,
        modalidad: null,
      },
      result: null,
      result1: null,
      result2: null,
      isetnia: false,
      isetnia1: false,
      isetnia2: false,
      modalidad: [
        { name: "Intensivo", id: "1" },
        { name: "Extraordinaria", id: "2" },
      ],
      ifLoad: null,
      mensaje: null,
    };
  },
  methods: {
    optenerEtnia() {
      this.isetnia = true;
      axios.get("https://pcei-app.herokuapp.com/api/etnias").then((result) => {
        this.result = result.data.datas;
        this.isetnia = false;
        
      });
    },
    optenerNacionalidad() {
      this.isetnia1 = true;
      axios
        .get("https://pcei-app.herokuapp.com/api/nacionalidad")
        .then((result) => {
          this.result1 = result.data.datas;
          this.isetnia1 = false;
        });
    },
    optenerParroquias() {
      this.isetnia2 = true;
      axios
        .get("https://pcei-app.herokuapp.com/api/parroquias")
        .then((result) => {
          this.result2 = result.data.datas;
          this.isetnia2 = false;
        });
    },
     save() {
      //-----------BOTTON DE GUADAR TIENE VALIDAR Y SI EL ID ES NULL ENTONCES GUARDA
     this.ifLoad = true;
          this.model.username = this.model.cedula;
          this.model.password = this.__getPasswods(
            this.model.apellidos,
            this.model.cedula
          );
          if (!this.model.status) {
            this.model.status = 0;
          }
           if(this.model.sexo==null||this.model.fkparroquia==null||this.model.fknacionalidad==null||this.model.fketnia==null||this.model.modalidad==null)
           {
               alert('COMPLETE TODOS LOS CAMPOS');
               this.ifLoad = false;
               return;
           }
          
          this.model.sexo = this.model.sexo.nombre;
          this.model.fkparroquia = this.model.fkparroquia.nombre;
          this.model.fknacionalidad = this.model.fknacionalidad.nombre;
          this.model.fketnia = this.model.fketnia.nombre;
          this.model.modalidad = this.model.modalidad.name;
         
          this.model.status = "1";
          //
              axios.post("https://pcei-app.herokuapp.com/api/estudiantes", this.model).then((result) => {
                console.log(result.data.savedUser);
                this.ifLoad = false;
                let id = result.data.savedUser._id //{ path: `/Registro2/${id}` }
                this.$router.push( {path: `/register2/${id}`})
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
     __getPasswods(apell, ced) {
      //-----------CREA LA CONTRASEÑAS PARA LOS USUARIOS EJMPLO {M1004095632}
      let l = apell.charAt(0);
      let result = l + ced;
      return result;
    },
      __validarCedula(event) {
      let ced = event.target.value;
      if (ced.length >= 10) {
        this.verificarCedula(ced);
      } else {
        this.mensaje = 'verifica tu cedula algo esta mal';
      }
    },
    verificarCedula(cedula) {
      if (cedula.length == 10) {
        var digito_region = cedula.substring(0, 2);
        if (digito_region >= 1 && digito_region <= 24) {
          var ultimo_digito = cedula.substring(9, 10);
          var pares =
            parseInt(cedula.substring(1, 2)) +
            parseInt(cedula.substring(3, 4)) +
            parseInt(cedula.substring(5, 6)) +
            parseInt(cedula.substring(7, 8));
          var numero1 = cedula.substring(0, 1);
          numero1 = numero1 * 2;
          if (numero1 > 9) {
            numero1 = numero1 - 9;
          }

          var numero3 = cedula.substring(2, 3);
          numero3 = numero3 * 2;
          if (numero3 > 9) {
            numero3 = numero3 - 9;
          }

          var numero5 = cedula.substring(4, 5);
          numero5 = numero5 * 2;
          if (numero5 > 9) {
            numero5 = numero5 - 9;
          }

          var numero7 = cedula.substring(6, 7);
          numero7 = numero7 * 2;
          if (numero7 > 9) {
            numero7 = numero7 - 9;
          }

          var numero9 = cedula.substring(8, 9);
          numero9 = numero9 * 2;
          if (numero9 > 9) {
            numero9 = numero9 - 9;
          }

          var impares = numero1 + numero3 + numero5 + numero7 + numero9;

          var suma_total = pares + impares;

          var primer_digito_suma = String(suma_total).substring(0, 1);

          var decena = (parseInt(primer_digito_suma) + 1) * 10;

          digito_validador = decena - suma_total;

          if (digito_validador == 10) var digito_validador = 0;
          if (digito_validador == ultimo_digito) {
            this.mensaje = "la cedula:" + cedula + " es correcta";
          } else {
            this.mensaje = "la cedula:" + cedula + " es incorrecta";
          }
        } else {
          this.mensaje = "Esta cedula no pertenece a ninguna region";
        }
      } else {
        this.mensaje = "Esta cedula tiene menos de 10 Digitos";
      }
    },
  },
  created() {
    this.optenerEtnia();
    this.optenerNacionalidad();
    this.optenerParroquias();
  },
};
</script>
<style></style>
