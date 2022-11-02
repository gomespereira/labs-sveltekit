<script>
  import { onMount } from 'svelte'
  import { goto } from '$app/navigation'
  import { page } from '$app/stores'

  onMount(() => {
    if (!$page.data.session) {
      goto('/signin')
    } else {
      goto('/dashboard')
    }
  })
</script>
