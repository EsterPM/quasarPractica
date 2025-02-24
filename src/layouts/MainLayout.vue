<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <q-toolbar-title> FLORENCIA - Recepción pedidos </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      show-if-above
      v-model="leftDrawerOpen"
      side="left"
      bordered
      class="bg-secondary scroll"
      width="60"
      :style="{ overflowY: 'auto', scrollbarWidth: 'none', msOverflowStyle: 'none' }"
    >
      <q-list>
        <EssentialLink v-for="(icon, index) in icons" :key="index" :icon="icon" />
      </q-list>
    </q-drawer>

    <q-page-container :style="{ paddingTop: '5px' }">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from 'vue'
import EssentialLink from 'src/components/EssentialLink.vue'

export default {
  components: {
    EssentialLink,
  },
  setup() {
    const leftDrawerOpen = ref(false)

    const icons = ref([
      'admin_panel_settings',
      'settings',
      'add_shopping_cart',
      'storefront',
      'bar_chart',
      'description',
      'point_of_sale',
      'euro',
      'open_in_full',
      'local_shipping',
      'inventory_2',
      'exit_to_app',
      'inventory',
      'production_quantity_limits',
      'autorenew',
      'restore',
      'flutter_dash',
      'request_quote',
      'construction',
    ])

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      icons,
    }
  },
}
</script>
