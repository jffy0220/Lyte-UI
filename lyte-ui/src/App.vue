<template>
  <v-app>
    <v-app-bar color="deep-purple" dark elevation="3" app>
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
      <v-toolbar-title>Lyte</v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group v-model="group" active-class="deep-purple--text text--accent-4">
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Dashboard</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-cart</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Orders</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-storefront</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Inventory</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-office-building</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Warehouse</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      
      <v-card class="d-flex mb-6" flat tile>
        <v-card class="pa-2" tile outline>
          <order-metric-list />
        </v-card>
        <v-card class="pa-2 align-self-start" outline tile>
          <order-table />
        </v-card>
        <v-card class="pa-2" outlined tile>
          <order-chat-widget />
        </v-card>
      </v-card>
      <v-card class="d-flex mb-6" flat tile>
        <v-card class="pa-2" tile outline>
          <order-navigation-menu />
        </v-card>
        <v-card class="pa-2 align-self-start" outline tile>
          <order-basic-metric-widget />
        </v-card>
        <v-card class="pa-2" tile outline>
          <order-processing-widget />
        </v-card>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
import OrderBasicMetricWidget from './components/Orders/Order-Basic-Metric-Widget.vue';
import OrderMetricList from './components/Orders/Order-Metric-List.vue';
import OrderNavigationMenu from './components/Orders/Order-Navigation-Menu.vue';
import OrderTable from './components/Orders/Order-Table.vue';
import OrderChatWidget from './components/Orders/OrderChatWidget.vue';
import OrderProcessingWidget from './components/Orders/OrderProcessingWidget.vue';

export default {
  components: { OrderTable, OrderMetricList, OrderNavigationMenu, OrderChatWidget, OrderBasicMetricWidget, OrderProcessingWidget },
  name: 'App',
  data: () => ({
    drawer: false,
    group: null
  })
};
</script>
