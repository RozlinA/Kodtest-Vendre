<script setup lang="ts">
import type { IApiResponse } from '@/models/IApiResponse';
import type { IEmployee } from '@/models/IEmployee';
import { onMounted, ref } from 'vue';
import EmployeePresentation from './EmployeePresentation.vue';

const employees = ref<IEmployee[]>([]);

const currentPage = ref(1);

const getEmployees = async (page: number) => {
  const response = await fetch(`https://reqres.in/api/users?page=${page}`);
  const data: IApiResponse = await response.json();
  employees.value = data.data;
}

onMounted(async () => {
  getEmployees(currentPage.value)
});

const handlePage = () => {
  if(currentPage.value === 1){
    currentPage.value++;
     getEmployees(currentPage.value);
  }
  else{
    currentPage.value--;
    getEmployees(currentPage.value);
  }
}
</script>

<template>
  <section class="employeeSection">
    <h1>Our team</h1>
    <div class="employeeWrapper">
      <article v-for="employee in employees" :key="employee.id" class="employeeContainer">
        <EmployeePresentation :employee="employee"></EmployeePresentation>
      </article>
    </div>
    <button @click="handlePage">{{ currentPage == 1 ? "Go to page 2" : "Go to page 1" }}</button>
  </section>
</template>

<style scoped>
  .employeeSection {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .employeeContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 5px;
  }

  h1 {
    font-size: 64px;
    font-weight: bold;
    padding-bottom: 50px;
    color: black;
  }

  button {
    background-color: #5333ED;
    color: white;
    font-size: 16px;
    padding: 18px 70px;
    border-radius: 10px;
    border: none;
    margin-top: 48px;
    font-weight: bold;
    cursor: pointer;
  }

  @media screen and (min-width: 600px) {
    .employeeWrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 50px;
  }
  }

  @media screen and (min-width: 768px) {
    .employeeWrapper {
      grid-template-columns: repeat(3, 1fr); 
    }
  } 

</style>