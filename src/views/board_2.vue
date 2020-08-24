<template>
  <v-row justify="space-around">
    <v-col>
      <v-card>
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
          <v-row justify="space-around">
            <v-col justify="center">
              <div>
                intentos
              </div>
            </v-col>
            <v-col justify="center">
              <div>
                puntaje
              </div>
            </v-col>
            <v-col justify="center">
              <div>
                cronometro
              </div>
            </v-col>
          </v-row>
        </v-card>
        <v-row justify="center">
          <v-col>
            <v-card class="mx-auto" max-width="600">
              <v-img
                class="white--text align-end"
                height="400px"
                width="578"
                src="https://t1.ea.ltmcdn.com/es/images/7/0/0/buhos_24007_1_600.jpg"
              >
                <!--https://upload.wikimedia.org/wikipedia/commons/7/7e/Enicognathus_leptorhynchus_-two_captive-8a.jpg https://t1.ea.ltmcdn.com/es/images/7/0/0/buhos_24007_1_600.jpg-->
              </v-img>
              <!--  <v-card-subtitle class="pb-0">Number 10</v-card-subtitle>  -->
              <v-card-text class="text--primary">
                <div>Tu respuesta:</div>
                <v-text-field :rules="rules"></v-text-field>
              </v-card-text>

              <v-card-actions>
                <v-btn color="orange" text>
                  Comprobar
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>

          <v-col>
            <v-row align="start" justify="space-around">
              <div>
                <v-btn color="orange" type="submit">
                  Pedir pista
                </v-btn>
              </div>
            </v-row>

            <v-row align="center" justify="space-around">
              <div>
                <v-sheet class="mx-auto" elevation="3" max-width="800">
                  <v-slide-group
                    v-model="model"
                    class="pa-4"
                    :multiple="multiple"
                    :show-arrows="showArrows"
                    :center-active="centerActive"
                  >
                    <v-slide-item
                      v-for="n in 5"
                      :key="n"
                      v-slot:default="{ active, toggle }"
                    >
                      <v-card
                        :color="active ? 'primary' : 'grey lighten-1'"
                        class="ma-4"
                        height="150"
                        width="150"
                        @click="toggle"
                        >sdfsdfsdf
                        <v-row
                          class="fill-height"
                          align="center"
                          justify="center"
                        >
                          <v-scale-transition>
                            <v-icon
                              v-if="active"
                              color="white"
                              size="48"
                              v-text="aaadasdfshdsnxcbdfa"
                            ></v-icon>
                          </v-scale-transition>
                        </v-row>
                      </v-card>
                    </v-slide-item>
                  </v-slide-group>
                </v-sheet>
              </div>
            </v-row>
          </v-col>

          <!--<v-card class="mx-auto" max-width="400">
            <v-container fluid class="pa-0">
              <v-row align="center">
                
              </v-row>
            </v-container>
          </v-card>-->
        </v-row>
      </v-card>

      <v-row>
        <v-col> </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>
<script>
export default {
  //el: "#app",
  data: () => ({
    tiempo: 0,
    rules: [
      //value => !!value || 'Required.',
      //(value) => (value || "").length <= 20 || "Max 20 characters",
      (value) => {
        //const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        //return pattern.test(value) || "Invalid answer.";
      },
    ],
    model: null,
    multiple: true,
    showArrows: true,
    centerActive: false,
    prevIcon: true,
    nextIcon: true,
  }),
  methods: {
    aumentar() {
      this.tiempo++;
    },
    actualizar() {
      this.aumentar();
      window.requestAnimtionFrame(this.actualizar);
    },
  },
};
//app.actualizar();
</script>
