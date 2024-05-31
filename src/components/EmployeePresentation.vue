<script setup lang="ts">
import type { IEmployee } from '@/models/IEmployee';

  
  interface EmployeeProps {
    employee: IEmployee;
  }

  defineProps<EmployeeProps>();

</script>

<template>
  <img :src="employee.avatar" alt="picture of employee">
  <h6>{{ employee.first_name + " " + employee.last_name }}</h6>
  <a :href="'mailto:' + employee.email">
      <i class="bi bi-envelope" :title="employee.email"</i>
  </a>
</template>

<style scoped>
  img {
    width: 180px;
    height: 180px;
    border-radius: 50%;
    object-fit: cover;
    margin-bottom: 5px;
 }

 h6 {
  font-size: 18px;
 }

 i {
  font-size: 25px;
 }

 i:hover {
  color: rgb(69, 165, 236);
 }
</style>