<script lang="ts">
  import { goto } from '$app/navigation'
  import { supabaseClient } from '$lib/supabaseClient'

  let loading: boolean = false
  let email: string
  let password: string

  async function handleSignUp() {
    try {
      loading = true
      const { error } = await supabaseClient.auth.signUp({ email, password })

      if (error) throw error

      alert('Sign up successful!')
      goto('/dashboard')
    } catch (error) {
      if (error instanceof Error) alert(error.message)
    } finally {
      loading = false
    }
  }
</script>

<svelte:head>
  <title>Sign Up - Sveltekit Labs</title>
  <meta name="description" content="Sveltekit Labs sign up page">
</svelte:head>

<div>
  <div>
    <h2>Sign up</h2>

    <p>
      or
      <a href="/signin">sign in</a>
    </p>
  </div>

  <form on:submit|preventDefault={handleSignUp}>
    <div>
      <label for="email">Email</label>
      <input
        bind:value={email}
        id="email"
        name="email"
        type="email"
        autocomplete="email"
        required
      >
    </div>

    <div>
      <label for="password">Password</label>
      <input
        bind:value={password}
        id="password"
        name="password"
        type="password"
        autocomplete="password"
        required
      >
    </div>

    <button type="submit">Sign up</button>
  </form>
</div>
