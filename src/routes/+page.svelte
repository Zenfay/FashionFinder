<script>
    import bg from '$lib/assets/NikePic.jpg';
    import { goto } from '$app/navigation';
    const handleClick = () => {
        goto('/login');
    }

    const hc = () => {
        goto('/register');
    }
</script>



<div class="container">
    <!-- svelte-ignore a11y-img-redundant-alt -->
    <img src={bg} alt="Background Image"/>
    <div class="overlay">
        <h1>Fashion Finder</h1>
        <h2>Unique clothes for a unique you</h2>
        <div class="login-container">
            <button on:click = {handleClick}>Login</button>
            <button on:click = {hc}>Sign Up</button>

        </div>
        
        
    </div>
</div>

<body>
    
</body>

<style global>
    @import './src/global.css';
    
    .overlay {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        text-align: center;
        color: white;
    }
    h1 {
        font-family: 'Arial', sans-serif;
        font-size: 4em;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    }
    h2 {
        font-family: 'Arial', sans-serif;
        font-size: 2em;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
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
    
    
</style>
