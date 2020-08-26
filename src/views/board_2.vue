<template>
  <v-row justify="space-around">
    <v-col>
      <v-card>
        <v-container fluid>
          <v-row justify="space-around">
            <v-col>
              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title class="space-around"
                    >Adivina la imagen</v-list-item-title
                  >
                  <v-list-item-subtitle
                    >Tema: aves endémicas</v-list-item-subtitle
                  >
                </v-list-item-content>
              </v-list-item>
            </v-col>
          </v-row>
          <v-card>
            <v-row justify="center" align="center">
              <v-col>
                <div>{{ intentos }} de 2</div>
                <div>
                  INTENTOS
                </div>
              </v-col>
              <v-col>
                <div id="numPuntos" class="numIndicador">
                  {{ puntaje }}
                </div>
                <div>
                  PUNTOS
                </div>
              </v-col>
              <v-col>
                <div>
                  {{ tiempo }}
                </div>
                <div>
                  TIEMPO
                </div>
              </v-col>
            </v-row>
          </v-card>
          <v-row justify="center">
            <v-col>
              <v-row justify="center">
                <v-card class="mx-auto">
                  <v-img
                    id="img"
                    class="blur6"
                    height="400px"
                    width="578"
                    src="https://t1.ea.ltmcdn.com/es/images/7/0/0/buhos_24007_1_600.jpg"
                  >
                  </v-img>
                  <v-card-text class="text--primary">
                    <div>Tu respuesta:</div>
                    <v-text-field
                      :rules="rules"
                      @click="actualizar"
                    ></v-text-field>
                  </v-card-text>

                  <v-card-actions>
                    <v-btn v-on:click="intento" color="orange" text>
                      Comprobar
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-row>
            </v-col>

            <v-col>
              <v-sheet class="mx-auto" elevation="3" width="650">
                <v-row align="center" justify="center">
                  <div>
                    <v-btn color="orange" type="submit" @click="verPista">
                      Pedir pista
                    </v-btn>
                  </div>
                </v-row>

                <v-row align="center" justify="space-around">
                  <v-slide-group
                    v-model="model"
                    class="pa-4"
                    :multiple="multiple"
                    :show-arrows="showArrows"
                    :center-active="centerActive"
                  >
                    <v-slide-item
                      v-for="(item, n) in items"
                      :key="n"
                      v-slot:default="{ active, toggle }"
                    >
                      <v-card
                        :color="active ? 'primary' : 'grey lighten-1'"
                        class="ma-4"
                        height="150"
                        width="150"
                        @click="toggle"
                      >
                        <v-row
                          class="fill-height"
                          align="center"
                          justify="center"
                          @click="verPista"
                        >
                          <v-scale-transition>
                            <v-icon
                              v-if="active"
                              align="center"
                              justify="center"
                              color="white"
                              size="20"
                              v-text="item.pista"
                            ></v-icon>
                          </v-scale-transition>
                        </v-row>
                      </v-card>
                    </v-slide-item>
                  </v-slide-group>
                </v-row>
                <!--  
                 <v-container fluid>
                  <v-row dense>
                    <v-col v-for="(item, n) in items" :key="n" :cols="4">
                      <v-card
                        :color="active ? 'primary' : 'grey lighten-1'"
                        class="ma-4"
                        height="150"
                        width="150"
                        @click="toggle"
                        :cols="4"
                      >
                        <v-row
                          class="fill-height"
                          align="center"
                          justify="center"
                        >
                          <v-scale-transition>
                            <v-icon
                              v-if="active"
                              align="center"
                              justify="center"
                              color="white"
                              size="20"
                              v-text="item.pista"
                            ></v-icon>
                          </v-scale-transition>
                        </v-row>
                      </v-card>
                    </v-col>
                  </v-row>
                </v-container>
                -->
              </v-sheet>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
      <v-row>
        <v-col> </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>
<script>
export default {

  data: () => ({
    b: 6,
    item: 1,
    tiempo: 0,
    rules: [
      /*
      value => !!value || 'Required.',
      (value) => (value || "").length <= 20 || "Max 20 characters",
      (value) => {
        const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return pattern.test(value) || "Invalid answer.";
      },
      */
    ],
    model: null,
    multiple: true,
    showArrows: true,
    centerActive: false,
    prevIcon: true,
    nextIcon: true,
    //
    puntaje: 100,
    intentos: 0,
    items: [
      {
        pista: "Tiene ojos muy grandes",
      },
      {
        pista: "Tiene plumas que parecen orejas",
      },
      {
        pista: "Puede girar la cabeza en 270°",
      },
      {
        pista: "Es un ave rapaz de hábitos nocturnos",
      },
      {
        pista: "Muchos la confunden con la lechuza",
      },
    ],
  }),
  methods: {
    verPista() {
      if (this.b > 1) {
        this.b--;
        document.getElementById("img").className = "blur" + this.b;
      }
      if (this.puntaje > 50) {
        this.puntaje -= 10;
      }
    },
    intento() {
      if (this.intentos < 2) {
        this.intentos++;
      }
    },
    aumentar() {
      this.tiempo++;
    },
    actualizar() {
      this.aumentar();
      window.requestAnimtionFrame(this.actualizar);
    },
  },
};
</script>
<style>
.blur6 {
  filter: blur(30px);
  -webkit-filter: blur(30px);
  -moz-filter: blur(30px);
  -o-filter: blur(30px);
  -ms-filter: blur(30px);
}
.blur5 {
  filter: blur(25px);
  -webkit-filter: blur(25px);
  -moz-filter: blur(25px);
  -o-filter: blur(25px);
  -ms-filter: blur(25px);
}
.blur4 {
  filter: blur(20px);
  -webkit-filter: blur(20px);
  -moz-filter: blur(20px);
  -o-filter: blur(20px);
  -ms-filter: blur(20px);
}
.blur3 {
  filter: blur(15px);
  -webkit-filter: blur(15px);
  -moz-filter: blur(15px);
  -o-filter: blur(15px);
  -ms-filter: blur(15px);
}
.blur2 {
  filter: blur(10);
  -webkit-filter: blur(10px);
  -moz-filter: blur(10);
  -o-filter: blur(10);
  -ms-filter: blur(10);
}
.blur1 {
  filter: blur(0px);
  -webkit-filter: blur(0px);
  -moz-filter: blur(0px);
  -o-filter: blur(0px);
  -ms-filter: blur(0px);
}
</style>
