// +page.server.js
import { fail, redirect } from '@sveltejs/kit';

/** @type {import('./$types').Actions} */
export const actions = {
  default: async ({ request }) => {
    const data = await request.formData();
    const nome = data.get('nome');
    const idade = data.get('idade');
    const linguagem = data.get('linguagem');

    console.log('[PADRÃO] Dados recebidos:', { nome, idade, linguagem });

    if (!nome || !idade || !linguagem) {
      return fail(400, { missing: true });
    }

    throw redirect(303, '/sucesso');
  },

  adicionarLivro: async ({ request }) => {
    const data = await request.formData();
    const titulo = data.get('titulo');
    const autor = data.get('autor');

    console.log('[ADICIONAR LIVRO]', { titulo, autor });

    if (!titulo || !autor) {
      return fail(400, { missing: true });
    }

    throw redirect(303, '/livros');
  },

  enviarMensagem: async ({ request }) => {
    const data = await request.formData();
    const mensagem = data.get('mensagem');
    const email = data.get('email');

    console.log('[ENVIAR MENSAGEM]', { mensagem, email });

    if (!mensagem || !email) {
      return fail(400, { missing: true });
    }

    throw redirect(303, '/contato');
  },

  registrarEvento: async ({ request }) => {
    const data = await request.formData();
    const evento = data.get('evento');
    const dataEvento = data.get('dataEvento');

    console.log('[REGISTRAR EVENTO]', { evento, dataEvento });

    if (!evento || !dataEvento) {
      return fail(400, { missing: true });
    }

    throw redirect(303, '/eventos');
  },

  inscreverCurso: async ({ request }) => {
    const data = await request.formData();
    const curso = data.get('curso');
    const aluno = data.get('aluno');

    console.log('[INSCREVER CURSO]', { curso, aluno });

    if (!curso || !aluno) {
      return fail(400, { missing: true });
    }

    throw redirect(303, '/cursos');
  }
};

// +page.svelte
<script>
  export let form;
</script>

<h1>Ações Nomeadas</h1>

<section>
  <h2>Formulário Padrão</h2>
  <form method="POST">
    <input name="nome" placeholder="Nome" />
    <input name="idade" placeholder="Idade" type="number" />
    <input name="linguagem" placeholder="Linguagem favorita" />
    <button type="submit">Enviar</button>
  </form>
</section>

<hr />

<section>
  <h2>Adicionar Livro</h2>
  <form method="POST" action="?/adicionarLivro">
    <input name="titulo" placeholder="Título do livro" />
    <input name="autor" placeholder="Autor do livro" />
    <button type="submit">Adicionar</button>
  </form>
</section>

<hr />

<section>
  <h2>Enviar Mensagem</h2>
  <form method="POST" action="?/enviarMensagem">
    <textarea name="mensagem" placeholder="Sua mensagem"></textarea>
    <input name="email" placeholder="Seu e-mail" type="email" />
    <button type="submit">Enviar</button>
  </form>
</section>

<hr />

<section>
  <h2>Registrar Evento</h2>
  <form method="POST" action="?/registrarEvento">
    <input name="evento" placeholder="Nome do evento" />
    <input name="dataEvento" placeholder="Data" type="date" />
    <button type="submit">Registrar</button>
  </form>
</section>

<hr />

<section>
  <h2>Inscrever em Curso</h2>
  <form method="POST" action="?/inscreverCurso">
    <input name="curso" placeholder="Nome do curso" />
    <input name="aluno" placeholder="Nome do aluno" />
    <button type="submit">Inscrever</button>
  </form>
</section>


// src/routes/exemplo/+page.server.js
import { fail, redirect } from '@sveltejs/kit';

/** @type {import('./$types').Actions} */
export const actions = {
  login: async ({ request }) => {
    const data = await request.formData();
    const email = data.get('email');
    const password = data.get('password');

    console.log('[LOGIN]', { email, password });

    if (!email || !password) {
      return fail(400, { missing: true });
    }

    // Simulação de login
    if (email === 'teste@email.com' && password === '123') {
      throw redirect(303, '/dashboard');
    }

    return fail(401, { invalid: true });
  },

  signup: async ({ request }) => {
    const data = await request.formData();
    const name = data.get('name');
    const email = data.get('email');
    const password = data.get('password');

    console.log('[SIGNUP]', { name, email, password });

    if (!name || !email || !password) {
      return fail(400, { missing: true });
    }

    // Simulação de criação de conta
    throw redirect(303, '/welcome');
  }
};


<!-- src/routes/exemplo/+page.svelte -->
<script>
  import { invalidate } from '$app/navigation';
  export let form;
</script>

<h1>Ações Nomeadas — Login e Cadastro</h1>

<section>
  <h2>Login</h2>
  <form method="POST" action="?/login">
    <label for="login-email">Email:</label>
    <input id="login-email" name="email" type="email" required />

    <label for="login-password">Senha:</label>
    <input id="login-password" name="password" type="password" required />

    <button type="submit">Entrar</button>
  </form>
  {#if form?.invalid}
    <p style="color:red">Email ou senha inválidos.</p>
  {/if}
  {#if form?.missing}
    <p style="color:red">Preencha todos os campos do login.</p>
  {/if}
</section>

<hr />

<section>
  <h2>Cadastro</h2>
  <form method="POST" action="?/signup">
    <label for="signup-name">Nome:</label>
    <input id="signup-name" name="name" type="text" required />

    <label for="signup-email">Email:</label>
    <input id="signup-email" name="email" type="email" required />

    <label for="signup-password">Senha:</label>
    <input id="signup-password" name="password" type="password" required />

    <button type="submit">Cadastrar</button>
  </form>
  {#if form?.missing}
    <p style="color:red">Preencha todos os campos do cadastro.</p>
  {/if}
</section>

Gerenciamento de Perfil de Usuário (src/routes/07/perfil)

<script>
  import { page } from '$app/stores';
  let { form } = $props();

  $: status = $page.url.searchParams.get('status');
</script>

<form method="POST">
  <label>
    Nome: <input name="nome" type="text" value={form?.nome ?? ''} />
  </label><br/>

  <label>
    E-mail: <input name="email" type="email" value={form?.email ?? ''} />
  </label><br/>

  <label>
    Senha Atual: <input name="senhaAtual" type="password" />
  </label><br/>

  <label>
    Nova Senha: <input name="novaSenha" type="password" />
  </label><br/>

  <label>
    Confirmar Nova Senha: <input name="confirmaSenha" type="password" />
  </label><br/>

  <label>
    <input type="checkbox" name="confirmarDesativacao" /> Confirmar desativação da conta
  </label><br/>

  <button type="submit" formaction="?/atualizarPerfil">Salvar Alterações</button>
  <button type="submit" formaction="?/alterarSenha">Alterar Senha</button>
  <button type="submit" formaction="?/desativarConta">Desativar Minha Conta</button>
</form>

{#if form?.error}
  <p style="color: red">{form.error}</p>
{/if}

{#if status === 'perfil_atualizado'}
  <p style="color: green">Perfil atualizado com sucesso!</p>
{/if}

{#if status === 'senha_alterada'}
  <p style="color: green">Senha alterada com sucesso!</p>
{/if}

import { fail, redirect } from '@sveltejs/kit';

export const actions = {
  atualizarPerfil: async ({ request }) => {
    const data = await request.formData();
    const nome = data.get('nome');
    const email = data.get('email');
    const senhaAtual = data.get('senhaAtual');

    if (!nome || !email || !senhaAtual) {
      return fail(400, { error: 'Nome, e-mail e senha atual são obrigatórios.', nome, email });
    }

    if (senhaAtual !== 'senhasecreta') {
      return fail(400, { error: 'Senha atual incorreta.', nome, email });
    }

    throw redirect(303, '/07/perfil?status=perfil_atualizado');
  },

  alterarSenha: async ({ request }) => {
    const data = await request.formData();
    const senhaAtual = data.get('senhaAtual');
    const novaSenha = data.get('novaSenha');
    const confirmaSenha = data.get('confirmaSenha');

    if (!senhaAtual || !novaSenha || !confirmaSenha) {
      return fail(400, { error: 'Todos os campos de senha são obrigatórios.' });
    }

    if (senhaAtual !== 'senhasecreta') {
      return fail(400, { error: 'Senha atual incorreta.' });
    }

    if (novaSenha !== confirmaSenha) {
      return fail(400, { error: 'Nova senha e confirmação não conferem.' });
    }

    if (novaSenha.length < 4) {
      return fail(400, { error: 'A nova senha deve ter ao menos 4 caracteres.' });
    }

    throw redirect(303, '/07/perfil?status=senha_alterada');
  },

  desativarConta: async ({ request }) => {
    const data = await request.formData();
    const senhaAtual = data.get('senhaAtual');
    const confirmarDesativacao = data.get('confirmarDesativacao');

    if (!confirmarDesativacao || senhaAtual !== 'senhasecreta') {
      return fail(400, { error: 'Você deve confirmar a desativação e fornecer a senha atual.' });
    }

    throw redirect(303, '/07/login?status=conta_desativada');
  }
};


<script>
  import { page } from '$app/stores';
  let status = '';

  $: status = $page.url.searchParams.get('status');
</script>

<h1>Login</h1>

{#if status === 'conta_desativada'}
  <p style="color: green">Conta desativada com sucesso. Volte sempre!</p>
{/if}

<form>
  <!-- campos de login aqui -->
</form>

Sistema de Gerenciamento de Conteúdo (CMS)

<script>
  import { page } from '$app/stores';
  let { form } = $props();

  $: id = $page.params.id;
</script>

<form method="POST">
  <input type="hidden" name="id" value={id} />

  <label>
    Título: <input name="titulo" type="text" value={form?.titulo ?? ''} />
  </label><br/>

  <label>
    Conteúdo:<br/>
    <textarea name="conteudo" rows="6">{form?.conteudo ?? ''}</textarea>
  </label><br/>

  <button type="submit" formaction="?/publicar">Publicar</button>
  <button type="submit" formaction="?/salvarRascunho">Salvar Rascunho</button>
  <button type="submit" formaction="?/excluir">Excluir Artigo</button>
</form>

{#if form?.error}
  <p style="color: red">{form.error}</p>
{/if}

{#if form?.success}
  <p style="color: green">{form.message}</p>
{/if}

import { fail, redirect } from '@sveltejs/kit';

export const actions = {
  publicar: async ({ request }) => {
    const data = await request.formData();
    const id = data.get('id');
    const titulo = data.get('titulo');
    const conteudo = data.get('conteudo');

    if (!id || !titulo || !conteudo) {
      return fail(400, { error: 'ID, título e conteúdo são obrigatórios.', titulo, conteudo });
    }

    // Lógica para publicar o artigo...

    throw redirect(303, `/07/blog/${id}?status=artigo_publicado`);
  },

  salvarRascunho: async ({ request }) => {
    const data = await request.formData();
    const titulo = data.get('titulo');

    if (!titulo) {
      return fail(400, { error: 'O título é obrigatório para salvar rascunho.' });
    }

    // Lógica para salvar rascunho...

    return { success: true, message: 'Rascunho salvo com sucesso!' };
  },

  excluir: async ({ request }) => {
    const data = await request.formData();
    const id = data.get('id');

    if (!id) {
      return fail(400, { error: 'ID do artigo é obrigatório para exclusão.' });
    }

    // Lógica para excluir o artigo...

    throw redirect(303, '/07/blog?status=artigo_excluido');
  }
};

<script>
  import { page } from '$app/stores';
  let status = '';
  $: status = $page.url.searchParams.get('status');
  let id = $page.params.id;

  // Dados fictícios do artigo
  let artigo = {
    id,
    titulo: 'Título Exemplo',
    conteudo: 'Conteúdo do artigo fictício...'
  };
</script>

<h1>{artigo.titulo}</h1>
<p>{artigo.conteudo}</p>

{#if status === 'artigo_publicado'}
  <p style="color: green">Artigo publicado com sucesso!</p>
{/if}

<script>
  import { page } from '$app/stores';
  let status = '';
  $: status = $page.url.searchParams.get('status');
</script>

<h1>Blog</h1>

{#if status === 'artigo_excluido'}
  <p style="color: green">Artigo excluído com sucesso!</p>
{/if}

<p>Lista de artigos (exemplo):</p>
<ul>
  <li><a href="/07/blog/1">Artigo 1</a></li>
  <li><a href="/07/blog/2">Artigo 2</a></li>
</ul>

Inscrição em Irmandades de Fantasia

<script>
  let { form } = $props();
</script>

<form method="POST">
  <label>
    Idade: <input name="idade" type="number" min="0" value={form?.idade ?? ''} required />
  </label><br/>

  <label>
    Força física (1 a 10): <input name="forca" type="number" min="1" max="10" value={form?.forca ?? ''} required />
  </label><br/>

  <label>
    Inteligência (1 a 10): <input name="inteligencia" type="number" min="1" max="10" value={form?.inteligencia ?? ''} required />
  </label><br/>

  <label>
    Destreza manual (1 a 10): <input name="destreza" type="number" min="1" max="10" value={form?.destreza ?? ''} required />
  </label><br/>

  <label>
    <input type="checkbox" name="conhecimentoMagia" checked={form?.conhecimentoMagia ?? false} /> Conhecimento de magia
  </label><br/>

  <label>
    <input type="checkbox" name="ferramentasArtesao" checked={form?.ferramentasArtesao ?? false} /> Ferramentas de artesão
  </label><br/>

  <button type="submit" formaction="?/juntarGuerreiros">Inscrever na Ordem dos Guerreiros</button>
  <button type="submit" formaction="?/juntarMagos">Inscrever no Círculo dos Magos</button>
  <button type="submit" formaction="?/juntarArtesaos">Inscrever na Guilda dos Artesãos</button>
</form>

{#if form?.error}
  <p style="color: red">{form.error}</p>
{/if}

import { fail, redirect } from '@sveltejs/kit';

export const actions = {
  juntarGuerreiros: async ({ request }) => {
    const data = await request.formData();
    const idade = Number(data.get('idade'));
    const forca = Number(data.get('forca'));

    if (idade < 18) {
      return fail(400, { error: 'Idade mínima para Guerreiros é 18 anos.', idade, forca });
    }

    if (forca < 7) {
      return fail(400, { error: 'Força mínima para Guerreiros é 7.', idade, forca });
    }

    throw redirect(303, '/07/irmandades/guerreiros');
  },

  juntarMagos: async ({ request }) => {
    const data = await request.formData();
    const idade = Number(data.get('idade'));
    const inteligencia = Number(data.get('inteligencia'));
    const conhecimentoMagia = data.get('conhecimentoMagia') === 'on';

    if (idade < 16) {
      return fail(400, { error: 'Idade mínima para Magos é 16 anos.', idade, inteligencia, conhecimentoMagia });
    }

    if (inteligencia < 8) {
      return fail(400, { error: 'Inteligência mínima para Magos é 8.', idade, inteligencia, conhecimentoMagia });
    }

    if (!conhecimentoMagia) {
      return fail(400, { error: 'Você deve possuir conhecimento de magia.', idade, inteligencia, conhecimentoMagia });
    }

    throw redirect(303, '/07/irmandades/magos');
  },

  juntarArtesaos: async ({ request }) => {
    const data = await request.formData();
    const idade = Number(data.get('idade'));
    const destreza = Number(data.get('destreza'));
    const ferramentasArtesao = data.get('ferramentasArtesao') === 'on';

    if (idade < 15) {
      return fail(400, { error: 'Idade mínima para Artesãos é 15 anos.', idade, destreza, ferramentasArtesao });
    }

    if (destreza < 6) {
      return fail(400, { error: 'Destreza mínima para Artesãos é 6.', idade, destreza, ferramentasArtesao });
    }

    if (!ferramentasArtesao) {
      return fail(400, { error: 'Você deve possuir ferramentas de artesão.', idade, destreza, ferramentasArtesao });
    }

    throw redirect(303, '/07/irmandades/artesaos');
  }
};

<h1>Bem-vindo à Ordem dos Guerreiros!</h1>
<p>Você é um verdadeiro guerreiro. Prepare-se para grandes desafios!</p>

Simulação de Solicitação de Empréstimo


<script>
  let { form } = $props();
</script>

<form method="POST">
  <label>
    Renda mensal (R$): <input name="renda" type="number" min="0" step="0.01" value={form?.renda ?? ''} required />
  </label><br/>

  <label>
    Score de crédito: <input name="score" type="number" min="0" max="1000" value={form?.score ?? ''} required />
  </label><br/>

  <label>
    <input type="checkbox" name="possuiImovel" checked={form?.possuiImovel ?? false} /> Possui imóvel para garantia
  </label><br/>

  <label>
    Valor do veículo (R$): <input name="valorVeiculo" type="number" min="0" step="0.01" value={form?.valorVeiculo ?? ''} />
  </label><br/>

  <button type="submit" formaction="?/solicitarPessoal">Solicitar Empréstimo Pessoal</button>
  <button type="submit" formaction="?/solicitarImobiliario">Solicitar Empréstimo Imobiliário</button>
  <button type="submit" formaction="?/solicitarAutomotivo">Solicitar Empréstimo Automotivo</button>
</form>

{#if form?.error}
  <p style="color: red">{form.error}</p>
{/if}


import { fail, redirect } from '@sveltejs/kit';

export const actions = {
  solicitarPessoal: async ({ request }) => {
    const data = await request.formData();
    const renda = Number(data.get('renda'));
    const score = Number(data.get('score'));

    if (isNaN(renda) || isNaN(score)) {
      return fail(400, { error: 'Renda e score devem ser números.', renda, score });
    }

    if (renda < 2000) {
      return fail(400, { error: 'Renda mensal mínima para empréstimo pessoal é R$ 2.000.', renda, score });
    }

    if (score < 600) {
      return fail(400, { error: 'Score mínimo para empréstimo pessoal é 600.', renda, score });
    }

    throw redirect(303, '/07/emprestimo/pessoal');
  },

  solicitarImobiliario: async ({ request }) => {
    const data = await request.formData();
    const renda = Number(data.get('renda'));
    const score = Number(data.get('score'));
    const possuiImovel = data.get('possuiImovel') === 'on';

    if (isNaN(renda) || isNaN(score)) {
      return fail(400, { error: 'Renda e score devem ser números.', renda, score, possuiImovel });
    }

    if (renda < 5000) {
      return fail(400, { error: 'Renda mensal mínima para empréstimo imobiliário é R$ 5.000.', renda, score, possuiImovel });
    }

    if (score < 700) {
      return fail(400, { error: 'Score mínimo para empréstimo imobiliário é 700.', renda, score, possuiImovel });
    }

    if (!possuiImovel) {
      return fail(400, { error: 'É necessário possuir imóvel para garantia.', renda, score, possuiImovel });
    }

    throw redirect(303, '/07/emprestimo/imobiliario');
  },

  solicitarAutomotivo: async ({ request }) => {
    const data = await request.formData();
    const renda = Number(data.get('renda'));
    const score = Number(data.get('score'));
    const valorVeiculo = Number(data.get('valorVeiculo'));

    if (isNaN(renda) || isNaN(score) || isNaN(valorVeiculo)) {
      return fail(400, { error: 'Renda, score e valor do veículo devem ser números.', renda, score, valorVeiculo });
    }

    if (renda < 3000) {
      return fail(400, { error: 'Renda mensal mínima para empréstimo automotivo é R$ 3.000.', renda, score, valorVeiculo });
    }

    if (score < 650) {
      return fail(400, { error: 'Score mínimo para empréstimo automotivo é 650.', renda, score, valorVeiculo });
    }

    if (valorVeiculo < 15000) {
      return fail(400, { error: 'Valor mínimo do veículo para financiamento é R$ 15.000.', renda, score, valorVeiculo });
    }

    throw redirect(303, '/07/emprestimo/automotivo');
  }
};


<h1>Empréstimo Pessoal</h1>
<p>Seu empréstimo pessoal foi aprovado! Em breve entraremos em contato.</p>




