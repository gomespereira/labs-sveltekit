<script lang="ts">
  import { goto } from '$app/navigation'
  import { page } from '$app/stores'
  import { supabaseClient } from '$lib/supabaseClient'

  let user = $page.data.session.user.email

  async function handleSignOut() {
    const { error } = await supabaseClient.auth.signOut()

    if (error) throw error

    alert('Signed out successful!')
    goto('/signin')
  }
</script>

<svelte:head>
  <title>Dashboard - Sveltekit Labs</title>
  <meta name="description" content="Sveltekit Labs dashboard page">
</svelte:head>

<h1>Dashboard</h1>

<div>Hello {user}!</div>

<button on:click={handleSignOut}>Sign out</button>
