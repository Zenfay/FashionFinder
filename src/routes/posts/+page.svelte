<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
    import bg from '$lib/assets/NikePic.jpg';
    import { goto } from '$app/navigation';

    let counter = 0;

    let photos = writable([]);
    let uploadedImage = writable(null);

    onMount(async () => {
        console.log("Fetching photos...");
        await fetchPhotos();
    });
    const handleClick = () => {
        goto('/');
    }
    
    
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
    function addTag(photo, tagInput) {
        const tag = tagInput.value.trim();
        if (tag && !photo.tags.includes(tag)) {
            photo.tags = [...photo.tags, tag]; // Create a new array
            photos.update(values => {
                return values.map(p => p.id === photo.id ? photo : p);
            });
        }
        tagInput.value = '';
    }


        function stringToColor(str) {
        let hash = 0;
        for (let i = 0; i < str.length; i++) {
            hash = str.charCodeAt(i) + ((hash << 5) - hash);
        }
        let color = '#';
        for (let i = 0; i < 3; i++) {
            const value = (hash >> (i * 8)) & 0xFF;
            color += ('00' + value.toString(16)).substr(-2);
        }
        return color;
    }

    let searchTag = '';
    let highlightedPhotos = [];

    $: highlightedPhotos = $photos.map(photo => ({
        ...photo,
        highlight: searchTag && photo.tags && photo.tags.includes(searchTag)
    }));

    function search() {
        // This function will be called when the search button is clicked
    }

    let imageUrls = [];

    function handleFileUpload(event) {
    const files = event.target.files;
    const reader = new FileReader();
    for (let i = 0; i < files.length; i++) {
        const file = files[i];
        reader.onloadend = () => {
            // Create a new photo object for the uploaded image
            const newPhoto = {
                id: Date.now(), // Use the current timestamp as a unique ID
                title: `Uploaded Image ${i + 1}`,
                thumbnailUrl: reader.result,
                tags: []
            };

            // Add the new photo to the photos store
            photos.update(values => [...values, newPhoto]);

            counter = counter + 1;
        };
        if (file) {
            reader.readAsDataURL(file);
        }
    }
}


</script>


<div class = "logout">
    <button on:click = {handleClick}>Log Out</button>
</div>

<div class="search">
    <input bind:value={searchTag} placeholder="Search by tag" />
    <button on:click={search}>Enter</button>
</div>

<div class="photos">
    {#each highlightedPhotos as photo (photo.id)}
    <!--.slice(0, counter)-->
        <figure class:highlight={photo.highlight}>
            <img src={photo.thumbnailUrl} alt="Uploaded Image" />
            {#if photo.tags && photo.tags.length}
                <div class="tags">
                    {#each photo.tags as tag (tag)}
                        <span class="tag" style="background-color: {stringToColor(tag)};">{tag}</span>
                    {/each}
                </div>
            {/if}
            <form on:submit|preventDefault={e => addTag(photo, e.target.elements.tag)}>
                <input name="tag" placeholder="Add a tag" />
                <button type="submit">Add
</button>
            </form>
        </figure>
    {:else}
        <p>loading...</p>
    {/each}
</div>

<div class="photos">
    {#each imageUrls as photo}
            <figure class:highlight={photo.highlight}>
                <img src={photo} alt="Uploaded Image" />
                {#if photo.tags && photo.tags.length}
                    <div class="tags">
                        {#each photo.tags as tag (tag)}
                            <span class="tag" style="background-color: {stringToColor(tag)};">{tag}</span>
                        {/each}
                    </div>
                {/if}
            <form on:submit|preventDefault={e => addTag(photo, e.target.elements.tag)}>
                <input name="tag" placeholder="Add a tag" />
                <button type="submit">Add
</button>
            </form>
        </figure>
    {/each}
</div>
  
  <div class="upload-button">
    <input type="file" accept="image/*" multiple on:change={handleFileUpload} />
  </div>
<body>

</body>
<style global>
    @import './src/global.css';
  .upload-button {
    margin-bottom: 20px;
  }
    .container {
        position: relative;
        width: 100%;
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
    .tags {
        margin-top: 5px;
    }

    .tag {
        display: inline-block;
        margin-right: 5px;
        padding: 2px 5px;
        background-color: #add8e6; /* light blue */
        color: black;
        border-radius: 3px;
        font-size: 12px;
    }
    .search {
        margin: 20px;
        text-align: center;
    }

    .search input {
        padding: 10px;
        font-size: 1em;
        border: 1px solid #ccc;
        border-radius: 4px;
    }

    .highlight {
        box-shadow: 0 0 10px #ff0000; /* red glow */
    }
</style>