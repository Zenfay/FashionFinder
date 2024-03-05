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
    <img class="bg" src={bg} alt="Background Image"/>
    <div class="overlay">
        <h1>Fashion Finder</h1>
        <h2>Unique clothes for a unique you</h2>
        <div class="login-container">
            <button on:click={handleClick}>Login</button>
            <button on:click={hc}>Sign Up</button>
        </div>
    </div>
</div>

<style global>
    @import './src/global.css';
    
    .bg {
        animation: zoom 10s ease-in-out infinite;
    }

    @keyframes zoom {
        0% {
            transform: scale(1);
        }
        50% {
            transform: scale(1.1);
        }
        100% {
            transform: scale(1);
        }
    }

    .overlay {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        text-align: center;
        color: white;
    }
    h1, h2 {
        font-family: 'Arial', sans-serif;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        animation: slide-in 2s ease-out;
    }
    h1 {
        font-size: 4em;
    }
    h2 {
        font-size: 2em;
    }

    @keyframes slide-in {
        0% {
            transform: translateX(-100%);
            opacity: 0;
        }
        100% {
            transform: translateX(0);
            opacity: 1;
        }
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
