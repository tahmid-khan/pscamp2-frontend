<script lang="ts">
  import UserAuthForm from "$lib/components/UserAuthForm.svelte";
</script>

<svelte:head>
  <title>PSCamp: Create your account</title>
  <meta name="description" content="Register for a PSCamp account" />
</svelte:head>

<UserAuthForm signinMode={false} />
