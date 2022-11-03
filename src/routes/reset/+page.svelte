<script lang="ts">
  import { supabaseClient } from '$lib/supabaseClient'

  let loading: boolean = false
  let email: string

  async function handleResetPassword() {
    try {
      loading = true
      const { error } = await supabaseClient.auth.resetPasswordForEmail(email, {
        redirectTo: 'https://labs-sveltekit.vercel.app/change'
      })

      if (error) throw error

      alert('If your email address exists in our database, you will receive a password recovery link in a few minutes.')
    } catch (error) {
      if (error instanceof Error) alert(error.message)
    } finally {
      loading = false
    }
  }
</script>

<svelte:head>
  <title>Reset your password - Sveltekit Labs</title>
  <meta name="description" content="Sveltekit Labs password reset page">
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
        <h2 class="mt-6 text-3xl font-bold tracking-tight text-gray-900">Reset your password</h2>
        <p class="mt-2 text-sm text-gray-600">
          Remembered? Try to
          <a href="/signin" class="font-medium text-indigo-600 hover:text-indigo-500">sign in</a>
          again.
        </p>
      </div>

      <div class="mt-8">
        <div class="mt-6">
          <form
            on:submit|preventDefault={handleResetPassword}
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
                  autocomplete="off"
                  required
                >
              </div>
            </div>

            <div>
              <button class="flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2" type="submit">Reset password</button>
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
