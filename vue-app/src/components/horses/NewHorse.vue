<script setup lang="ts">
import { Horse } from "../../shared/classes/Horse";
import HorseForm from "./HorseForm.vue";
import { HorseService } from "../../services/HorseService";
import type { AxiosStatic } from "axios";
import { Ref, inject, ref } from "vue";
import { IHorse } from "../../shared/interfaces/IHorse";
const emit = defineEmits(["created"]);
const axios: AxiosStatic | undefined = inject("axios");
const horseService = new HorseService(axios);
const newHorse: Ref<IHorse> = ref(new Horse());
const create = () => {
  horseService.create(newHorse.value).then(() => {
    emit("created");
  });
};
</script>
<template>
  <v-card-title>Neues Pferd </v-card-title>
  <v-card-text>
    <HorseForm v-model="newHorse"></HorseForm>
    <v-btn @click="create()">Speichern</v-btn>
  </v-card-text>
</template>
