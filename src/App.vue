<template>
  <Header/>
  <div class="container mt-5">
    <div class="col-md-8 offset-md-2">
      <Calendar/>
    </div>
  </div>
</template>

<script>
import Calendar from '@/components/Calender'
import Header from '@/components/Header'
export default {
  components:{
    Header,
    Calendar,
  },
};
</script>

<style>
body {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
