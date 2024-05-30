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

</style>