<template>
  <q-page padding>
    <div class="q-gutter-md col-md-6 col-sm-12">
      <h5 class="q-my-md">Restaurant Setup [cite: 30]</h5>
      
      <q-input v-model="restaurant.name" label="Restaurant Name" filled />
      <q-file v-model="restaurant.logo" label="Logo Upload" filled accept=".jpg, .png" />
      <q-input v-model="restaurant.address" label="Address" filled type="textarea" />
      <q-input v-model="restaurant.phone" label="Phone Number" filled />
      <q-input v-model="restaurant.branches" label="Branch Name(s)" filled placeholder="Separate with commas" />

      <div class="q-mt-lg">
        <q-btn label="Save Restaurant Info" color="primary" @click="saveInfo" />
        <q-btn label="Delete Info" color="negative" flat @click="deleteInfo" />
      </div>

      <q-separator class="q-my-lg" />

      <div class="row q-gutter-sm">
        <q-btn to="/items" label="All Items Page" color="secondary" />
        <q-btn to="/orders" label="Orders Page" color="secondary" />
        <q-btn to="/invoice" label="Invoice Page" color="secondary" />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useQuasar } from 'quasar';

const $q = useQuasar();
const restaurant = ref({
  name: '', logo: null, address: '', phone: '', branches: ''
});

// Save to Local Storage 
const saveInfo = () => {
  localStorage.setItem('restaurant_info', JSON.stringify(restaurant.value));
  $q.notify({ type: 'positive', message: 'Info Saved!' });
};

const deleteInfo = () => {
  localStorage.removeItem('restaurant_info');
  restaurant.value = { name: '', logo: null, address: '', phone: '', branches: '' };
  $q.notify({ type: 'warning', message: 'Info Deleted!' });
};

onMounted(() => {
  const saved = localStorage.getItem('restaurant_info');
  if (saved) restaurant.value = JSON.parse(saved);
});
</script>