<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" class="drawer" app>
      
      <v-list class="profile" dark>
        <v-list-item class="px-2">
          <v-list-item-avatar>
            <v-img src="https://s.gravatar.com/avatar/ffa25f3b30395a486d2ee572f16471f5?s=80"></v-img>
          </v-list-item-avatar>
        </v-list-item>

        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class>Luiz Alberto</v-list-item-title>
            <v-list-item-subtitle>Software Enginner</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <v-divider></v-divider>

      <v-list dense class="pt-0 mt-2" dark>
        <template v-for="item in items">
          
          <v-list-group class v-if="item.children" :key="item.text" v-model="item.model">
            <template v-slot:activator>
              <v-list-item-icon>
                <v-icon color="grey lighten-2">{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>{{ item.text }}</v-list-item-title>
              </v-list-item-content>
            </template>
            <v-list-item v-for="(child, i) in item.children" :key="i" class="menu-item" link>
              <v-list-item-icon v-if="child.icon">
                <v-icon color="grey lighten-2" dense>{{ child.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-content >
                <v-list-item-title>{{ child.text }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
          
          <v-list-item v-else :key="item.text" link class="menu-item">
            <v-list-item-icon>
              <v-icon color="grey lighten-2">{{ item.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>{{ item.text }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

        </template>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="#F3F3F4" :elevation="0" flat light>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title style="width: 300px" class="ml-0 pl-4">
        <span class="hidden-sm-and-down">MyTasq</span>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-select
        :items="balconys"
        label="Selecione um balcão"
        dense
        hide-details
        prepend-icon="mdi-map-marker"
        solo
      ></v-select>
      <v-btn icon>
        <v-icon>mdi-bell</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <div class="nuxt-content fill-height">
        <Nuxt />
      </div>
    </v-main>
    <v-btn bottom color="pink" dark fab fixed right @click="dialog = !dialog">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-dialog v-model="dialog" width="800px">
      <v-card>
        <v-card-title class="grey darken-2">Create contact</v-card-title>
        <v-container>
          <v-row class="mx-2">
            <v-col class="align-center justify-space-between" cols="12">
              <v-row align="center" class="mr-0">
                <v-avatar size="40px" class="mx-3">
                  <img src="//ssl.gstatic.com/s2/oz/images/sge/grey_silhouette.png" alt />
                </v-avatar>
                <v-text-field placeholder="Name"></v-text-field>
              </v-row>
            </v-col>
            <v-col cols="6">
              <v-text-field prepend-icon="mdi-account-card-details-outline" placeholder="Company"></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field placeholder="Job title"></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field prepend-icon="mdi-mail" placeholder="Email"></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field type="tel" prepend-icon="mdi-phone" placeholder="(000) 000 - 0000"></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field prepend-icon="mdi-text" placeholder="Notes"></v-text-field>
            </v-col>
          </v-row>
        </v-container>
        <v-card-actions>
          <v-btn text color="primary">More</v-btn>
          <v-spacer></v-spacer>
          <v-btn text color="primary" @click="dialog = false">Cancel</v-btn>
          <v-btn text @click="dialog = false">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<style>
.nuxt-content {
  background-color: #f3f3f4;
  flex-direction: column;
  align-content: flex-start;
}
.text-shadow {
  text-shadow: 1px 1px 3px #000000;
}
.drawer > div {
  background-color: #2f4050;
}

.v-list-group--active {
  background-color: rgba(0, 0, 0, 0.2);
  border-left: 4px solid #19aa8d;
}
.profile {
  background-image: url("https://ajrent.pt/ws/resources/theme/css/patterns/header-profile.png") !important;
  background-size: cover !important;
}
</style>

<script>
export default {
  props: {
    source: String,
  },
  data: () => ({
    dialog: false,
    drawer: null,
    balconys: ["Caldas da Rainha", "Torres Vedras", "Peniche"],
    items: [
      { icon: "mdi-view-dashboard", text: "Dashboard" },
      { icon: "mdi-calendar-edit", text: "Reservas" },
      { icon: "mdi-calendar-account", text: "Guias de transporte" },
      {
        icon: "mdi-account-group",
        text: "Utilizadores",

        children: [
          { icon: "mdi-plus", text: "Criar" },
          { icon: "mdi-plus", text: "Listar" },
          { icon: "mdi-plus", text: "Administradores" },
        ],
      },
      {
        icon: "mdi-domain",
        text: "Organizações",
        model: false,
        children: [
          { icon: "mdi-plus", text: "Import" },
          { icon: "mdi-plus", text: "Export" },
          { icon: "mdi-plus", text: "Print" },
          { icon: "mdi-plus", text: "Undo changes" },
          { icon: "mdi-plus", text: "Other contacts" },
        ],
      },
      { icon: "mdi-storefront", text: "Balcões" },
      { icon: "mdi-tools", text: "Manutenções" },
      { icon: "mdi-car", text: "Gestão de viaturas" },
      { icon: "mdi-cash-usd", text: "Tarifários" },
      { icon: "mdi-car-connected", text: "Via Verde" },
      { icon: "mdi-help-circle", text: "Ajuda" },
    ],
  }),
};
</script>