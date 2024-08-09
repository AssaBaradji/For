<template>
  <div id="app">
    <UserForm />
  </div>
</template>

<script>
import UserForm from './components/UserForm.vue';

export default {
  components: {
    UserForm
  }
};
</script>
<style>
body{
  background:rgb(192, 189, 189);
}
#app{
  display: flex;
  justify-content: center;
}
</style>