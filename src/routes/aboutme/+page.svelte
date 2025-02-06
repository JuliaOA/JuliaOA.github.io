<script>
  let linkedin = "https://www.linkedin.com";
  let instagram = "https://www.instagram.com";
  let github = "https://www.github.com";
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .container {
    font-family: 'Arial', sans-serif;
    color: #000;  /* Fonte preta */
    line-height: 1.6;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    padding: 20px;
    max-width: 900px;
    width: 100%;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    background-color: #fff; /* Fundo branco */
  }

  .container h1 {
    font-size: 2.5em;
    margin-bottom: 20px;
  }

  .container p {
    font-size: 1.1em;
    margin-bottom: 30px;  /* Aumentando o espaço entre os parágrafos */
    line-height: 1.8;
  }

  .img-container {
    margin-bottom: 20px;
    border-radius: 50%;
    overflow: hidden;
    width: 200%;
    height: auto;
    margin: 0 auto;
  }

  .img-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .social-icons {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 20px;
  }

  .social-icons a {
    text-decoration: none;
    color: #2c3e50;
    font-size: 1.5em;
    transition: color 0.3s;
  }

  .social-icons a:hover {
    color: #3498db;
  }

  @media (max-width: 768px) {
    .container {
      padding: 20px;
    }

    .container h1 {
      font-size: 2em;
    }

    .container p {
      font-size: 1em;
    }

    .img-container {
      width: auto;
      height: auto;
    }
  }
</style>

<div class="container">
  <div class="img-container">
    <img src="me.jpg" alt="Minha Foto">
  </div>
  <h1>Olá, eu sou Julia!</h1>
  <p>Sou estudante de ensino médio apaixonada por aprender e explorar novas áreas do conhecimento. Atualmente, estou me dedicando a estudar psicologia e direito, com o sonho de estudar no exterior.</p>
  <p>Além disso, sou muito interessada em temas de cultura, especialmente aqueles relacionados a questões sociais e raciais. Acredito que a educação é a chave para um futuro melhor para todos.</p>
  
  <div class="social-icons">
    <a href={linkedin} target="_blank">🔗</a>
    <a href={instagram} target="_blank">📷</a>
    <a href={github} target="_blank">🐙</a>
  </div>
</div>
