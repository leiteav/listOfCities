<template>
  <div>
    <h1>Cidades</h1>
    <ion-list>
      <div v-for="cidade in cidadesArray" :key="cidade.id">
        <p>Id: {{ cidade.id }}</p>
        <p>Nome: {{ cidade.nome }}</p>
        <hr />
      </div>
    </ion-list>
  </div>
</template>

<script lang="ts">
import { IonContent } from "@ionic/vue";
import { defineComponent } from "vue";
import axios from "axios";

export default defineComponent({
  name: "HomePage",
  data() {
    return {
      cidadesArray: [],
    };
  },
  beforeMount() {
    this.carregarCidades();
  },
  methods: {
    carregarCidades() {
      axios
        .get(
          "https://servicodados.ibge.gov.br/api/v1/localidades/estados/35/municipios"
        )
        .then((res) => this.mapearCidades(res.data))
        .catch((err) => console.log(err.data));
    },
    mapearCidades(value) {
      this.cidadesArray = value;
    },
  },
});
</script>

<style>
* {
  color: white;
}
hr {
  background-color: green;
  color: green;
}
div,
p,
h1 {
  margin: 0px 5px;
}
</style>
