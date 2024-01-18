<script lang="ts">
  import UserAuthForm from "$lib/components/UserAuthForm.svelte";
</script>

<svelte:head>
  <title>PSCamp: Sign in to your account</title>
  <meta name="description" content="Sign in to your PSCamp account" />
</svelte:head>

<UserAuthForm signinMode={true} />
