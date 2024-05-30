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
  .employeeSection {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .employeeWrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 50px;
  }

  .employeeContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  h1 {
    font-size: 64px;
    font-weight: bold;
    padding-bottom: 50px;
    color: black;
  }

  @media screen and (min-width: 768px) {
    .employeeWrapper {
      grid-template-columns: repeat(3, 1fr); 
    }
  } 

</style>