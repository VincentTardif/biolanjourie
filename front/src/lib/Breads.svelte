<script>
    const database = import.meta.env.VITE_API_BASE_URL + "items/Breads";
    // console.log(database);
    async function getBreads() {
        const response = await fetch("http://localhost:8055/items/Breads?fields=*,images.*", {
            method: "GET",
            headers: {
                "Content-Type": "application/json"
            }
        }
        )
        const json = await response.json();
        // console.log(json);
        return json.data
    }
    // getBreads();
</script>
<h1>Les bons pains <br>de Freddy et JeanMi</h1>

{#await getBreads()}
<p>Patiente un peu... J'interroge la base de données</p>
{:then breads}

{#each breads as bread}
<section class="bread">
    <div class="description">
        <h2>{bread.name} - {bread.price} €</h2>
        {bread.description}
    </div>
    <div class="picture">
        <img src={"http://localhost:8055/assets/" + bread.picture} alt="{bread.name}">
    </div>
</section>
{/each}

{:catch error}
  <p>erreur : {error.message}</p>
{/await}


