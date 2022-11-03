<script lang="ts">
  import { goto } from '$app/navigation'
  import { supabaseClient } from '$lib/supabaseClient'

  let loading: boolean = false
  let email: string
  let password: string
  let confirmPassword: string

  async function handleSignUp() {
    try {
      loading = true
      const { error } = await supabaseClient.auth.signUp({ email, password })

      if (error) throw error

      alert('Signed up successful!')
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
        <h2 class="mt-6 text-3xl font-bold tracking-tight text-gray-900">Sign up</h2>
        <p class="mt-2 text-sm text-gray-600">
          Already have an account?
          <a href="/signin" class="font-medium text-indigo-600 hover:text-indigo-500">Sign in</a>.
        </p>
      </div>

      <div class="mt-8">
        <div class="mt-6">
          <form
            on:submit|preventDefault={handleSignUp}
            class="space-y-6"
          >
            <div>
              <label for="email" class="block text-sm font-medium text-gray-700">Email address</label>
              <div class="mt-1">
                <input
                  bind:value={email}
                  class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  id="email"
                  name="email"
                  type="email"
                  autocomplete="off"
                  required
                >
              </div>
            </div>

            <div class="space-y-1">
              <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
              <div class="mt-1">
                <input
                  bind:value={password}
                  class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  id="password"
                  name="password"
                  type="password"
                  autocomplete="off"
                  required
                >
              </div>
            </div>

            <div class="space-y-1">
              <label for="confirm-password" class="block text-sm font-medium text-gray-700">Confirm password</label>
              <div class="mt-1">
                <input
                  bind:value={confirmPassword}
                  class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                  id="confirm-password"
                  name="confirm-password"
                  type="password"
                  autocomplete="off"
                  required
                >
              </div>
            </div>

            <p class="text-sm">
              By registering, you agree to the processing of your personal data as described in the
              <a href="/" class="font-medium text-indigo-600 hover:text-indigo-500">Privacy Policy</a>.
            </p>

            <div class="flex items-center">
              <input id="remember-me" name="remember-me" type="checkbox" class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
              <label for="remember-me" class="ml-2 block text-sm text-gray-900">
                I've read and agree to the
                <a href="/" class="font-medium text-indigo-600 hover:text-indigo-500">Terms of Service</a>.
              </label>
            </div>

            <div>
              <button type="submit" class="flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Sign up</button>
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
