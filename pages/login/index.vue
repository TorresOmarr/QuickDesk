<script setup lang="ts">
const { loggedIn, user, fetch: refreshSession } = useUserSession()
const credentials = reactive({
    email: '',
    password: '',
})
async function login() {
    try {
        await $fetch('/api/login', {
            method: 'POST',
            body: credentials
        })
        // Refresh the session on client-side and redirect to the home page
        await refreshSession()
        await navigateTo('/')
    } catch (error) {
        alert('Bad credentials')
    }
}
</script>

<template>
    <form @submit.prevent="login">
        <input v-model="credentials.email" type="email" placeholder="Email" />
        <input v-model="credentials.password" type="password" placeholder="Password" />
        <UButton color="secondary" @click="login">Login</UButton>
    </form>
</template>