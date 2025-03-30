<script>
    let pokemon = null;

    const getPokemon = async ()=>{
        let id = Math.floor(Math.random() * 300 - 1) + 1
        try {
            const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${id}`)
            const result = await response.json()
            pokemon = {...result}
        } catch (error) {
            console.log("Error al generar pokemon",error)
        }
    }

    getPokemon()
</script>

<main class="main">
    <div class="container">
        {#if pokemon}
        <div class="card">
            <h1 class="pokemon-name">{pokemon.name.toUpperCase()}</h1>
            <div class="image-container">
                <img class="pokemon-image" src={pokemon.sprites.other.dream_world.front_default} alt={pokemon.name}>
                <div class="glow-effect"></div>
            </div>
            <button class="change-btn" on:click={getPokemon}>Ver Otro Pokemon</button>
        </div>
        {:else}
        <div class="loading-container">
            <div class="loader"></div>
            <h2 class="loading">Buscando Pokemon...</h2>
        </div>
        {/if}
    </div>
</main>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        background-color: #121212;
        color: #ffffff;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .main {
        width: 100%;
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
    }

    .container {
        width: 90%;
        max-width: 800px;
        padding: 2rem;
    }

    .card {
        background: rgba(30, 30, 46, 0.8);
        backdrop-filter: blur(10px);
        border-radius: 20px;
        padding: 2rem;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        border: 1px solid rgba(255, 255, 255, 0.1);
        text-align: center;
        transition: transform 0.3s ease;
    }

    .card:hover {
        transform: translateY(-5px);
    }

    .pokemon-name {
        font-size: 2.5rem;
        margin-bottom: 1.5rem;
        color: #fff;
        text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
        letter-spacing: 2px;
        font-weight: 600;
    }

    .image-container {
        position: relative;
        margin: 1.5rem 0;
    }

    .pokemon-image {
        width: 300px;
        height: 300px;
        object-fit: contain;
        filter: drop-shadow(0 0 15px rgba(100, 149, 237, 0.5));
        transition: all 0.3s ease;
        z-index: 1;
        position: relative;
    }

    .pokemon-image:hover {
        transform: scale(1.05);
        filter: drop-shadow(0 0 20px rgba(100, 149, 237, 0.8));
    }

    .glow-effect {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 320px;
        height: 320px;
        background: radial-gradient(circle, rgba(100, 149, 237, 0.3) 0%, rgba(100, 149, 237, 0) 70%);
        border-radius: 50%;
        z-index: 0;
        animation: pulse 3s infinite alternate;
    }

    .change-btn {
        background: linear-gradient(45deg, #4a6cf7 0%, #2541b2 100%);
        color: white;
        border: none;
        padding: 12px 30px;
        font-size: 1rem;
        border-radius: 50px;
        cursor: pointer;
        margin-top: 1.5rem;
        transition: all 0.3s ease;
        box-shadow: 0 4px 15px rgba(37, 65, 178, 0.3);
        font-weight: 500;
        letter-spacing: 1px;
        text-transform: uppercase;
    }

    .change-btn:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(37, 65, 178, 0.4);
        background: linear-gradient(45deg, #5a7cff 0%, #3151d6 100%);
    }

    .change-btn:active {
        transform: translateY(0);
    }

    .loading-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .loader {
        border: 5px solid rgba(255, 255, 255, 0.1);
        border-top: 5px solid #4a6cf7;
        border-radius: 50%;
        width: 50px;
        height: 50px;
        animation: spin 1s linear infinite;
        margin-bottom: 1rem;
    }

    .loading {
        color: rgba(255, 255, 255, 0.8);
        font-weight: 300;
        letter-spacing: 1px;
    }

    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }

    @keyframes pulse {
        0% { opacity: 0.5; transform: translate(-50%, -50%) scale(0.95); }
        100% { opacity: 0.8; transform: translate(-50%, -50%) scale(1.05); }
    }

    @media (max-width: 768px) {
        .pokemon-image {
            width: 250px;
            height: 250px;
        }
        
        .glow-effect {
            width: 270px;
            height: 270px;
        }
        
        .pokemon-name {
            font-size: 2rem;
        }
    }
</style>