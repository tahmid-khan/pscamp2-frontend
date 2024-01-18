<script lang="ts">
  import { Icons } from "$lib/components/icons";
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import { Label } from "$lib/components/ui/label";
  import { Separator } from "$lib/components/ui/separator";
  import { Sun, Moon } from "radix-icons-svelte";
  import { toggleMode } from "mode-watcher";

  let isLoading = false;
  async function onSubmit() {
    isLoading = true;

    setTimeout(() => {
      isLoading = false;
    }, 3000);
  }

  export let signinMode: boolean;
</script>

<div
  class="container relative grid h-full flex-col items-center justify-center lg:max-w-none lg:grid-cols-2 lg:px-0"
>
  <Button
    on:click={toggleMode}
    variant="ghost"
    size="icon"
    class="absolute right-4 top-4 md:right-8 md:top-8"
  >
    <Sun
      class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
      alt="sun"
    />
    <Moon
      class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
      alt="moon"
    />
    <span class="sr-only">Toggle theme</span>
  </Button>

  <div class="relative hidden h-full flex-col bg-muted p-10 text-white lg:flex dark:border-r">
    <div
      class="absolute inset-0 bg-cover"
      style="
        background-image:
          url(https://images.unsplash.com/photo-1590069261209-f8e9b8642343?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1376&q=80);"
    />
    <div class="relative z-20 flex items-center text-lg font-medium">
      <!-- <Command class="mr-2 h-6 w-6" /> -->
      <h1><strong>PSCamp</strong> by NSUPS</h1>
    </div>
    <div class="relative z-20 mt-auto">
      <blockquote class="space-y-2">
        <p class="text-lg">
          &ldquo;This library has saved me countless hours of work and helped me deliver stunning
          designs to my clients faster than ever before. Highly recommended!&rdquo;
        </p>
        <footer class="text-sm">Sofia Davis</footer>
      </blockquote>
    </div>
  </div>
  <div class="lg:p-8">
    <div class="mx-auto flex w-full flex-col justify-center space-y-6 sm:w-[398px]">
      <div class="flex flex-col space-y-2 text-center">
        <h2 class="text-2xl font-semibold tracking-tight">
          {signinMode ? "Sign in to" : "Create"} your account
        </h2>
      </div>

      <form on:submit|preventDefault={onSubmit}>
        <div class="grid gap-4 space-y-1 px-6">
          {#if !signinMode}
            <p class="mb-2 text-sm text-muted-foreground">Use your NSU email address.</p>
          {/if}
          <div class="grid gap-2">
            <Label for="email">Email address</Label>
            <Input
              id="email"
              type="email"
              placeholder="name@northsouth.edu"
              autocomplete="email"
              required
            />
          </div>
          <div class="grid gap-2">
            <Label for="password">Password</Label>
            <Input id="password" type="password" autocomplete="current-password" required />
          </div>
          <Button type="submit" disabled={isLoading} class="mt-2">
            {#if isLoading}
              <Icons.spinner class="mr-2 h-4 w-4 animate-spin" />
            {/if}
            Sign {signinMode ? "in" : "up"}
          </Button>
          <div class="relative mt-2">
            <div class="absolute inset-0 flex items-center">
              <span class="w-full border-t" />
            </div>
            <div class="relative flex justify-center text-xs uppercase">
              <span class="bg-card px-2 text-muted-foreground">
                Or sign {signinMode ? "in" : "up"} with
              </span>
            </div>
          </div>
          <div class="grid grid-cols-2 gap-6">
            <Button variant="outline">
              <Icons.gitHub class="mr-2 h-4 w-4" />GitHub
            </Button>
            <Button variant="outline">
              <Icons.google class="mr-2 h-4 w-4" />Google
            </Button>
          </div>
        </div>

        <Separator orientation="horizontal" class="mb-6 mt-8" />

        <div class="grid space-y-2 px-6">
          <p class="px-8 text-center text-sm text-muted-foreground">
            {#if signinMode}
              Not registered yet?
            {:else}
              Already registered?
            {/if}
          </p>
          <Button variant="ghost" href={signinMode ? "/register" : "/signin"}>
            {#if signinMode}
              Create your account
            {:else}
              Sign in instead
            {/if}
          </Button>
        </div>
      </form>
    </div>
  </div>
</div>
