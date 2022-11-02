<script lang="ts">
  import { goto } from '$app/navigation'
  import { supabaseClient } from '$lib/supabaseClient'

  let loading: boolean = false
  let email: string
  let password: string

  async function handleSignIn() {
    try {
      loading = true
      const { error } = await supabaseClient.auth.signInWithPassword({ email, password })

      if (error) throw error

      alert('Sign in successful!')
      goto('/dashboard')
    } catch (error) {
      if (error instanceof Error) alert(error.message)
    } finally {
      loading = false
    }
  }
</script>

<svelte:head>
  <title>Sign In - Sveltekit Labs</title>
  <meta name="description" content="Sveltekit Labs sign in page ">
</svelte:head>

<div>
  <div>
    <h2>Sign in</h2>

    <p>
      or
      <a href="/signup">sign up</a>
    </p>
  </div>

  <form on:submit|preventDefault={handleSignIn}>
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

    <button type="submit">Sign in</button>
  </form>
</div>
