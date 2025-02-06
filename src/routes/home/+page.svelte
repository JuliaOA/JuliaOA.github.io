<div style="margin: 50px 0 90px 0;">
    <div class="text-center mb-4">
        <img src="Design sem nome.png" alt="Imagem de destaque" class="img-fluid" style="width: 700px; max-height: 500px ;" />
    </div>
    </div>
   


<script>
    import { blog } from '$lib/blog.js';

    let pesquisa = '';
    let filtrados = blog;

    function atualizarPesquisa(event) {
        pesquisa = event.target.value.toLowerCase();
        filtrados = blog.filter(post => post.título.toLowerCase().includes(pesquisa));
    }
</script>


<div class="row align-items-center mb-3" >
    <div class="col">
        <input on:input={atualizarPesquisa} class="form-control" placeholder="Pesquisar artigos..." />
    </div>
</div>



<div class="row g-4" style="margin-top: 30px;">
    {#each filtrados as post}
        <div class="col-md-6 col-xl-3">
            <div class="card h-100">
                <img src={post.imagem} class="card-img-top" alt="Imagem do post" />
                <div class="card-body">
                    <h5 class="card-title">{post.título}</h5>
                    <h6 class="card-subtitle mb-2 text-body-secondary">{post.publicado}</h6>
                    <p class="card-text">{post.sinopse}</p>
                    <a href="{post.referência}" target="_blank" rel="noopener noreferrer" class="btn btn-primary">
                        Ler mais
                    </a>
                </div>
            </div>
        </div>
    {/each}
</div>

<style>
    .card {
        display: flex;
        flex-direction: row;
        width: 100%;
        max-width: 600px;
        max-height: 300px;
        margin: 10px auto;
        border-radius: 10px;
        overflow: hidden;
        box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
    }

    .card img {
        max-width: 40%;
        height: auto;
        object-fit: cover;
    }

    .card-body {
        width: 80%;
        padding: 20px;
    }
</style>
