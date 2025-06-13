<script setup lang="ts">
import { ref } from 'vue'

const email = ref('')
const password = ref('')

// Debug function to check values
const debugValues = () => {
  console.log('Email ref value:', email.value)
  console.log('Password ref value:', password.value)
}

const handleSignIn = async () => {
  // Debug the values before creating user object
  debugValues()

  // Validate that fields are not empty
  if (!email.value.trim() || !password.value.trim()) {
    alert('Please fill in both email and password')
    return
  }

  const user = {
    email: email.value.trim(),
    password: password.value,
  }

  console.log('User object:', user)

  try {
    const response = await fetch('http://localhost:3000/api/user/sign-in', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(user),
    })

    console.log('Response status:', response.status)
    const data = await response.json()
    console.log('Response data:', data)
  } catch (error) {
    console.error('Error:', error)
  }
}
</script>

<template>
  <form class="sign-in-form" @submit.prevent="handleSignIn">
    <label>Logga in</label>
    <input type="email" placeholder="E-mailadress" v-model="email" required autocomplete="email" />
    <input
      type="password"
      placeholder="Lösenord"
      v-model="password"
      required
      autocomplete="current-password"
    />
    <button type="submit">Logga in</button>
  </form>
</template>

<style lang="css" scoped>
.sign-in-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.sign-in-form input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.sign-in-form button {
  padding: 10px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.sign-in-form button:hover {
  background: #0056b3;
}
</style>
