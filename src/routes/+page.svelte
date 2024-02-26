<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
    import bg from '$lib/assets/NikePic.jpg';
    import { goto } from '$app/navigation';
    let username = '';
    let password = '';


    let photos = writable([]);

    onMount(async () => {
        console.log("Fetching photos...");
        await fetchPhotos();
    });

    
    async function fetchPhotos() {
        try {
            const res = await fetch('/photos.json');
            console.log("Response status:", res.status);

            if (res.ok) {
                const photosData = await res.json();
                photos.set(photosData); // Update the value of the writable store
                console.log("Photos:", photosData);
            } else {
                console.error("Failed to fetch photos:", res.statusText);
            }
        } catch (error) {
            console.error("Error fetching photos:", error);
        }
    }
</script>



<div class="container">
    <img src={bg} alt="Background Image"/>
    <div class="overlay">
        <h1>Fashion Finder</h1>
        <h2>Unique clothes for a unique you</h2>
        <div class="login-container">
            <h1>Login</h1>
            <input bind:value={username} placeholder="Username" />
            <input bind:value={password} type="password" placeholder="Password" />
            <button>Login</button>
        </div>
        
    </div>
</div>

<div class="photos">
    {#each $photos as photo}
        <figure>
            <img src={photo.thumbnailUrl} alt={photo.title} />
            <figcaption>{photo.title}</figcaption>
        </figure>
    {:else}
        <p>loading...</p>
    {/each}
</div>
<style>
    .container {
        position: relative;
        width: 100%;
    }
    .login-container {
        display: flex;
        flex-direction: column;
        width: 300px;
        margin: 0 auto;
        padding: 20px;
    }
    input {
        margin-bottom: 10px;
        padding: 10px;
        font-size: 1em;
        border: 1px solid #ccc;
        border-radius: 4px;
    }
    .photos {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }

    .photos figure {
        margin: 10px;
        text-align: center;
    }

    .photos img {
        max-width: 200px;
        height: auto;
        border-radius: 5px;
    }

    .photos figcaption {
        margin-top: 5px;
        font-size: 14px;
    }
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
