<script>
    let username = '';
    let password = '';
</script>

<div class="login-container">
    <h1>Login</h1>
    <input bind:value={username} placeholder="Username" />
    <input bind:value={password} type="password" placeholder="Password" />
    <button>Login</button>
</div>

<style>
    .login-container {
        display: flex;
        flex-direction: column;
        width: 300px;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 4px;
    }
    h1 {
        text-align: center;
        font-family: 'Arial', sans-serif;
    }
    input {
        margin-bottom: 10px;
        padding: 10px;
        font-size: 1em;
        border: 1px solid #ccc;
        border-radius: 4px;
    }
    button {
        padding: 10px;
        font-size: 1em;
        background-color: #007BFF;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }
    button:hover {
        background-color: #0056b3;
    }
</style>


