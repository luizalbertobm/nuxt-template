<template>
  <div>
    <h1>Teste</h1>

    <v-container>
      <v-expansion-panels class="mb-3" :elevation="0">
        <v-expansion-panel >
          <v-expansion-panel-header>
            <v-badge bordered color="info" overlap inline :content="3" :value="3">Veículos no pátio</v-badge>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-data-table
              :headers="headers"
              :items="desserts"
              :single-expand="singleExpand"
              :expanded.sync="expanded"
              item-key="name"
              show-expand
              class="elevation-1"
            >
              <template v-slot:top>
                <v-toolbar flat>
                  <v-toolbar-title>Expandable Table</v-toolbar-title>
                  <v-spacer></v-spacer>
                  <v-switch v-model="singleExpand" label="Single expand" class="mt-2"></v-switch>
                </v-toolbar>
              </template>
              <template v-slot:expanded-item="{ headers, item }">
                <td
                  :colspan="headers.length"
                  style="background-color:#ffff99"
                >More info about {{ item.name }}</td>
              </template>
            </v-data-table>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-container>

    <v-form>
      <v-row class="box2">
        <v-col cols="12" sm="6">
          <v-text-field dense v-model="message4" label="Nome" outlined clearable></v-text-field>
        </v-col>
        <v-col cols="12" sm="6">
          <v-text-field dense v-model="message4" label="E-mail" outlined clearable></v-text-field>
        </v-col>
        <v-col cols="12" sm="6">
          <v-text-field dense v-model="message4" label="Telefone" outlined clearable></v-text-field>
        </v-col>
        <v-col cols="12" sm="6">
          <v-text-field dense v-model="message4" label="Teste" outlined clearable></v-text-field>
        </v-col>
      </v-row>
    </v-form>

    <div class="links">
      <a
        href="https://nuxtjs.org/"
        target="_blank"
        rel="noopener noreferrer"
        class="button--green"
      >Documentation</a>
      <a
        href="https://github.com/nuxt/nuxt.js"
        target="_blank"
        rel="noopener noreferrer"
        class="button--grey"
      >GitHub</a>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default {
  data() {
    return {
      expanded: [],
      singleExpand: false,
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
        { text: "", value: "data-table-expand" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%",
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: "7%",
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: "8%",
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: "16%",
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: "0%",
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: "2%",
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: "45%",
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: "22%",
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: "6%",
        },
      ],
    };
  },
};

//export default Vue.extend({});
</script>

<style>
h1 {
  border-top: 1px solid #e9e9e9;
  border-bottom: 1px solid #e9e9e9;
  background-color: white;
  margin-bottom: 20px;
  padding: 15px;
  font-weight: 300;
}
.box2 {
  border-top: 3px solid #e9e9e9;
  background-color: white;
  padding: 15px;
  margin: 15px;
}
</style>
