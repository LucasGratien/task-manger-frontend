<template>
  <div class="login-container">
    <div class="form-wrapper">
      <form @submit.prevent="handleSubmit" class="login-form">
        <h2 class="form-title">Bienvenue</h2>
        <div class="input-group">
          <label for="email">Pseudo</label>
          <input
            v-model="pseudo"
            id="pseudo"
            type="pseudo"
            placeholder="Entrez votre pseudo"
            required
          />
        </div>
        <div class="input-group">
          <label for="password">Mot de passe</label>
          <div class="password-input">
            <input
              v-model="password"
              id="password"
              :type="showPassword ? 'text' : 'password'"
              placeholder="Entrez votre mot de passe"
              required
            />
            <button
              type="button"
              class="toggle-password"
              @click="togglePasswordVisibility"
            >
              <EyeIcon v-if="showPassword" />
              <EyeOffIcon v-else />
            </button>
          </div>
        </div>
        <div class="form-options">
          <div class="remember-me">
            <input id="remember-me" type="checkbox" />
            <label for="remember-me">Se souvenir de moi</label>
          </div>
          <a href="#" class="forgot-password">Mot de passe oublié ?</a>
        </div>
        <button type="submit" class="submit-button">Se connecter</button>
        <p class="signup-link">
          Vous n'avez pas de compte ?
          <a href="#">S'inscrire</a>
        </p>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { EyeIcon, EyeOffIcon } from 'lucide-vue-next'

const pseudo = ref('')
const password = ref('')
const showPassword = ref(false)

const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value
}

const handleSubmit = () => {
  console.log('Tentative de connexion avec:', { email: pseudo.value, password: password.value })
}
</script>

<style scoped>
.login-container {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(to bottom right, #9f7aea, #f687b3);
  padding: 1rem;
}

.form-wrapper {
  width: 100%;
  max-width: 28rem;
}

.login-form {
  background-color: white;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  border-radius: 0.5rem;
  padding: 2rem;
}

.form-title {
  font-size: 1.875rem;
  font-weight: bold;
  text-align: center;
  color: #8314c4;
  margin-bottom: 2rem;
}

.input-group {
  margin-bottom: 1.5rem;
}

.input-group label {
  display: block;
  font-size: 0.875rem;
  font-weight: bold;
  color: #8314c4;
  margin-bottom: 0.5rem;
}

.input-group input {
  width: 100%;
  padding: 0.75rem 0.50rem;
  font-size: 1rem;
  color: #4a5568;
  background-color: white;
  border: 1px solid #e2e8f0;
  border-radius: 0.25rem;
  transition: all 0.3s;
}

.input-group input:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(159, 122, 234, 0.3);
  border-color: #9f7aea;
}

.password-input {
  position: relative;
}

.toggle-password {
  position: absolute;
  right: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  color: #718096;
  cursor: pointer;
}

.form-options {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.remember-me {
  display: flex;
  align-items: center;
}

.remember-me input {
  margin-right: 0.5rem;
}

.remember-me label {
  font-size: 0.875rem;
  color: #4a5568;
}

.forgot-password {
  font-size: 0.875rem;
  color: #9f7aea;
  text-decoration: none;
  font-weight: 500;
}

.forgot-password:hover {
  color: #805ad5;
}

.submit-button {
  width: 100%;
  background-color: #9f7aea;
  color: white;
  font-weight: bold;
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 0.25rem;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s;
}

.submit-button:hover {
  background-color: #805ad5;
  transform: scale(1.05);
}

.submit-button:active {
  transform: scale(0.95);
}

.signup-link {
  text-align: center;
  font-size: 0.875rem;
  color: #4a5568;
  margin-top: 1.5rem;
}

.signup-link a {
  color: #9f7aea;
  font-weight: 500;
  text-decoration: none;
}

.signup-link a:hover {
  color: #805ad5;
}
</style>
