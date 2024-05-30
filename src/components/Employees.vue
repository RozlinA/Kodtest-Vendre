<script setup lang="ts">
/* __placeholder__ */
import type { IApiResponse } from '@/models/IApiResponse';
import type { IEmployee } from '@/models/IEmployee';
import { onMounted, ref } from 'vue';
import EmployeePresentation from './EmployeePresentation.vue';


const employees = ref<IEmployee[]>([]);

  onMounted(async () => {
    const response = await fetch("https://reqres.in/api/users");
    const data: IApiResponse = await response.json();
    employees.value = data.data;
    console.log(data.data)
  });

</script>

<template>
  <section class="employeeSection">
    <h1>Our team</h1>
    <div class="employeeWrapper">
      <article v-for="employee in employees" :key="employee.id" class="employeeContainer">
        <EmployeePresentation :employee="employee"></EmployeePresentation>
      </article>
    </div>
  </section>
</template>

<style scoped>

</style>