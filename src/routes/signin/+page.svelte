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

      alert('Signed in successful!')
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
  <meta name="description" content="Sveltekit Labs sign in page">
</svelte:head>

<div class="flex min-h-screen">
  <div class="flex flex-1 flex-col justify-center py-12 px-4 sm:px-6 lg:flex-none lg:px-20 xl:px-24">
    <div class="mx-auto w-full max-w-sm lg:w-96">
      <div>
        <img
          class="h-12 w-auto"
          src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=600"
          alt="Company logo"
          loading="eager"
        >
        <h2 class="mt-6 text-3xl font-bold tracking-tight text-gray-900">Sign in</h2>
        <p class="mt-2 text-sm text-gray-600">
          New here?
          <a href="/signup" class="font-medium text-indigo-600 hover:text-indigo-500">Sign up for an account</a>.
        </p>
      </div>

      <div class="mt-8">
        <div class="mt-6">
          <form
            on:submit|preventDefault={handleSignIn}
            class="space-y-6"
          >
            <div>
              <label class="block text-sm font-medium text-gray-700" for="email">Email address</label>
              <div class="mt-1">
                <input
                  bind:value={email}
                  class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  id="email"
                  name="email"
                  type="email"
                  autocomplete="email"
                  required
                >
              </div>
            </div>

            <div class="space-y-1">
              <label class="block text-sm font-medium text-gray-700" for="password">Password</label>
              <div class="mt-1">
                <input
                  bind:value={password}
                  class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  id="password"
                  name="password"
                  type="password"
                  autocomplete="current-password"
                  required
                >
              </div>
            </div>

            <div class="text-sm">
              <a class="font-medium text-indigo-600 hover:text-indigo-500" href="/reset">Forgot your password?</a>
            </div>

            <div>
              <button class="flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2" type="submit">Sign in</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
  <div class="relative hidden w-0 flex-1 lg:block">
    <img
      class="absolute inset-0 h-full w-full object-cover"
      src="https://images.unsplash.com/photo-1505904267569-f02eaeb45a4c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1908&q=80"
      alt="Modern construction"
      loading="eager"
    >
  </div>
</div>
