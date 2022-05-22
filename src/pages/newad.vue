<template>
  <q-page>
    <div v-if="storeN.data" class="row justify-center">
      <div class="col-12 col-sm-8 col-md-6 col-lg-4">
        <q-form @submit="onSubmit">
          <h5 class="text-center q-mt-sm q-mb-none">
            Add new advertisement ({{ Object.keys(storeN.data).length }})
          </h5>
          <q-select
            v-model="storeN.data.kategoriaId"
            clearable
            emit-value
            filled
            label="Kategória"
            map-options
            option-label="megnevezes"
            option-value="id"
            :options="store1.data1"
            :rules="[(v) => v != null || 'Please choose one!']"
          />
          <q-input
            v-model="storeN.data.hirdetesDatuma"
            clearable
            filled
            label="Dátum"
            :rules="[(v) => (v != null && v != '') || 'dateField - Choose!']"
            type="date"
          />
          <q-input
            v-model="storeN.data.leiras"
            filled
            label="Leírás"
            :rules="[(v) => (v != null && v != '') || 'Please fill in!']"
            thousands-separator=" "
            type="textarea"
          />
          <q-input
            v-model="storeN.data.kepUrl"
            clearable
            filled
            label="Kép URL"
            :rules="[(v) => (v != null && v != '') || 'Please fill in!']"
            type="url"
          />
          <q-checkbox v-model="storeN.data.tehermentes" label="Tehermentes" />
          <div class="row justify-center">
            <q-btn class="q-mr-md" color="blue" label="Submit" no-caps type="submit" />
          </div>
        </q-form>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
  import { useStore1 } from "../store/store1";
  import { useStoreN } from "../store/storeN";
  import { date } from "quasar";
  import router from "src/router";

  const storeN = useStoreN();
  const store1 = useStore1();

  onMounted(() => {
    store1.getAll();
    storeN.getAll();
    storeN.data = {};
  });

  function onSubmit() {
    storeN.create();
  }
</script>

<style lang="scss" scoped></style>
