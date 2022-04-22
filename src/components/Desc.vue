<template>
    
    <div id="card">
        <div >
            
            <p class="container">Formulario de cadastro de contato</p>
            <form id="formulario" @submit="createContact">
                <div class="container">
                    <label for="name">Nome do contato</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="digite seu nome">
                </div>
                <div class="container">
                    <label for="numero">numero do contato</label>
                    <input type="text" id="numero" name="numero" v-model="numero" placeholder="digite seu numero">
                </div>
                <div class="container">
                    <label for="email">email do contato</label>
                    <input type="text" id="email" name="email" v-model="email" placeholder="digite seu email">
                </div>
                <div class="container">
                    <input type="submit" class="btn-criar" value="criar contato">
                    
                </div>
            </form>
        </div>
    </div>
</template>


<script>

export default {
    name: "Desc",
    data() {
        return {
            name: null,
            email: null,
            numero: null,
            msg: null
        }
    }
}

</script>