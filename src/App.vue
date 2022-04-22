<template>
  <div >
    <div>
      <router-link to="/">Lista de Contatos</router-link> |
      <router-link to="/descricao">Descricao de um contato</router-link> |
      <router-link to="/formulario">formulário para Adicionar um contato</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
body {
  display: flex;
  justify-content: center
}
</style>