<script setup lang="ts">
/* __placeholder__ */
import type { IApiResponse } from '@/models/IApiResponse';
import type { IEmployee } from '@/models/IEmployee';
import { onMounted, ref } from 'vue';


const employees = ref<IEmployee[]>([]);

  onMounted(async () => {
    const response = await fetch("https://reqres.in/api/users");
    const data: IApiResponse = await response.json();
    employees.value = data.data;
    console.log(data.data)
  });

</script>

<template>

</template>

<style scoped>

</style>