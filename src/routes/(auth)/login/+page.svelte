<script lang="ts">
    import type { ActionData } from './$types'
  
    export let form: ActionData
  </script>
  
  <h1>Login</h1>
  
  <form action="?/login" method="POST">
    <div>
      <label for="username">Username</label>
      <input id="username" name="username" type="text" required />
    </div>
  
    <div>
      <label for="password">Password</label>
      <input id="password" name="password" type="password" required />
    </div>
  
    {#if form?.invalid}
      <p class="error">Username and password is required.</p>
    {/if}
  
    {#if form?.credentials}
      <p class="error">You have entered the wrong credentials.</p>
    {/if}
  
    <button type="submit">Log in</button>
  </form>
<style>
    input {
        margin-bottom: 10px;
        padding: 10px;
        font-size: 1em;
        border: 1px solid #ccc;
        border-radius: 4px;
    }
    button {
        display: inline-block;
        margin-top: 20px;
        padding: 10px 20px;
        font-size: 1.5em;
        color: white;
        background-color: #007BFF;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        text-shadow: none;
    }
    button:hover {
        background-color: #0056b3;
    }
    h1 {
        font-family: 'Arial', sans-serif;
        font-size: 4em;
        text-shadow: 2px 2px 4px white;
    }
</style>