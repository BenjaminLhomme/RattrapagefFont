<script lang="ts">
    import { onMount } from 'svelte';

    type User = {
        Id: number;
        Email: string;
        Password: string;
    };

    let user: User | null = null;
  
    async function fetchUser() {
      const token = localStorage.getItem("jwt");
      if (!token) {
        location.href = "/login";
        return;
      }
  
      const response = await fetch("/api/users", {
        headers: {
          "Authorization": `Bearer ${token}`
        }
      });
  
      user = await response.json();
    }
  
    onMount(fetchUser);
</script>
  
{#if user}
    <h1>Gestion de l'utilisateur</h1>
    <p>Email: {user.Email}</p>
    <!-- Ajoutez ici d'autres champs et fonctionnalités CRUD -->
{:else}
    <p>Chargement...</p>
{/if}
