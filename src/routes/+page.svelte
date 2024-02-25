<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
    import bg from '$lib/assets/NikePic.jpg';
    import { goto } from '$app/navigation';

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
        <button on:click={() => goto('/login')}>Login</button>
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
    img {
        display: block;
        width: 100%;
        height: auto;
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
