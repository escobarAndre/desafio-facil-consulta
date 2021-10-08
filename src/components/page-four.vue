<template>
  <div>
    <div id="form" class="pt-5 pb-1 px-5 shadow text-center">
      <h2>Conclusão do cadastro</h2>
      <p>Obrigado por se cadastrar na Fácil Consulta!!</p>
      <div id="imgs" class="container d-flex">
        <img src="../assets/desktop-pagina-1.png" alt="" />
        <img src="../assets/desktop-pagina-2.png" alt="" />
        <img src="../assets/desktop-pagina-3.png" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
</script>

<style scoped>
#form {
  width: 65vw;
  height: 25rem;
  background-color: #ffffff;
  border-radius: 1rem;
  margin: 0 auto;
  margin-top: 7rem;
  left: 17%;
  top: 3.5%;
}

h2 {
  color: #483698;
  height: 2rem;
}

p {
  color: #282828;
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

#imgs{
    margin: 2rem 0;
}

img {
  width: 35%;
  height: auto;
}

@media (max-width: 480px) {
  #form {
    width: 100vw;
    height: 95vh;
    background-color: #ffffff;
    border-radius: 5rem 5rem 0 0 ;
    margin: 0 auto;
    padding: 3rem 1rem!important;
  }

  h2{
    text-align: center;
    padding: 0;
    margin: 5rem 0;
    height: 1rem;
  }

  #imgs{
    display: inline-block!important;
  }

  img{
    width: 50%;
  }


}
</style>