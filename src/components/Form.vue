<template>
    
    <div id="card">
        <Message :msg="msg" v-show="msg" />
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

import Message from '../components/Message.vue'

export default {
    name: "Form",
    data() {
        return {
            name: null,
            email: null,
            numero: null,
            msg: null
        }
    },
    methods: {
        async createContact(e) {
            e.preventDefault();

            const data = {
                name: this.name,
                email: this.email,
                numero: this.numero
            }

            const dataJson = JSON.stringify(data)    
            const req = await fetch("http://localhost:3000/contacts", {
                method: "POST",
                headers: { "Content-Type" : "application/json" },
                body: dataJson
            });
                const res = await req.json()

                this.msg = "Contato criado com sucesso!"

                setTimeout(() => this.msg = "", 2000)

                this.name = ""
                this.email = ""
                this.numero = ""


        }
    },
  components: {
    Message
  
    }
}
</script>


<style scoped>

#card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #F2F3F4;
    width: 600px;
    border-radius: 8px;
}

#formulario {
    max-width: 500px;
    margin: 0 auto;
}

.container {
    display: flex;
    flex-direction: column;
    margin-bottom: 10px;
}

label {
    font-weight: bold;
    margin-bottom: 8px;
    color: #222;;
    padding: 5px 10px;
}
  
input {
    padding: 5px 10px;
    width: 300px;
     margin-bottom: 12px;
}

.btn-criar {
    background-color: #3498DB;
    color: #fff;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    width: 150px;
}

.btn-criar:hover {
background-color: #277ACF;
color: #444;
}


</style>