<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Restaurant POS System
        </q-toolbar-title>

        <q-btn
          flat
          round
          :icon="$q.dark.isActive ? 'light_mode' : 'dark_mode'"
          @click="$q.dark.toggle()"
        />
        <div class="q-ml-md">Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label header>
          Navigation
        </q-item-label>

        <q-item 
          v-for="nav in navigationLinks" 
          :key="nav.title" 
          clickable 
          v-ripple 
          :to="nav.link"
        >
          <q-item-section avatar>
            <q-icon :name="nav.icon" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ nav.title }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'

// Updated link list to match Step 2 & Step 3 requirements [cite: 41, 45, 54, 64]
const navigationLinks = [
  {
    title: 'Restaurant Setup',
    icon: 'storefront',
    link: '/setup'
  },
  {
    title: 'All Items',
    icon: 'restaurant_menu',
    link: '/items'
  },
  {
    title: 'Orders',
    icon: 'shopping_cart',
    link: '/orders'
  },
  {
    title: 'Invoices',
    icon: 'receipt_long',
    link: '/invoice'
  }
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>