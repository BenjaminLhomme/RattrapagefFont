<script>
    import { onMount } from 'svelte';
    let email = "";
    let password = "";
  
    async function login() {
      const response = await fetch("/api/auth/login", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ email, password })
      });
  
      const data = await response.json();
      if (data.Token) {
        localStorage.setItem("jwt", data.Token);
        location.href = "/user";
      } else {
        alert("Erreur de connexion");
      }
    }
  </script>
  
  <form on:submit|preventDefault={login}>
    <input type="email" bind:value={email} placeholder="Email" required>
    <input type="password" bind:value={password} placeholder="Mot de passe" required>
    <button type="submit">Se connecter</button>
  </form>
  