<template>
  <div>
    <h2>Formulaire d'Informations Utilisateur</h2>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Nom:</label>
        <input type="text" v-model="name" />
        <span v-if="errors.name">{{ errors.name }}</span>
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="email" />
        <span v-if="errors.email">{{ errors.email }}</span>
      </div>
      <div>
        <label for="phone">Téléphone:</label>
        <input type="tel" v-model="phone" />
        <span v-if="errors.phone">{{ errors.phone }}</span>
      </div>
      <button type="submit">Soumettre</button>
    </form>
    <p v-if="successMessage">{{ successMessage }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const name = ref('');
const email = ref('');
const phone = ref('');
const errors = ref({});
const successMessage = ref('');

const validateEmail = (email) => {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return re.test(email);
};

const submitForm = () => {
  errors.value = {};
  successMessage.value = '';

  if (!name.value) {
    errors.value.name = 'Le nom est requis';
  }
  if (!email.value) {
    errors.value.email = 'L\'email est requis';
  } else if (!validateEmail(email.value)) {
    errors.value.email = 'L\'email est invalide';
  }
  if (!phone.value) {
    errors.value.phone = 'Le numéro de téléphone est requis';
  }

  if (Object.keys(errors.value).length === 0) {
    successMessage.value = 'Formulaire soumis avec succès!';
  }
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  border: 1px solid rgb(192, 189, 189);
  padding: 20px;
  background-color: white;
}
div {
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
}
div input {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid rgb(192, 189, 189);
}
span {
  color: red;
}
.successMessage {
  color: green;
}
button {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: none;
  margin-top: 20px;
}
</style>
