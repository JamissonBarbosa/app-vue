<template>
  <div id="burger-table" v-if="contacts">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Nome:</div>
        <div>Email:</div>
        <div>Numero:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="contact in contacts" :key="contact.id">
        <div class="order-number">{{ contact.id }}</div>
        <div>{{ contact.name }}</div>
        <div>{{ contact.email }}</div>
        <div>{{ contact.numero }}</div>
        
        <div>
          <button class="edit-btn" @click="updateBurger($event, )">Editar</button>
        </div>

        <div>
          <button class="delete-btn" @click="deleteBurger(contact.id)">Excluir</button>
        </div>

      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há pedidos no momento!</h2>
  </div>
</template>


<script>
  export default {
    name: "List",
    data() {
      return {
        contacts: null,
        contact_id: null,
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch('http://localhost:3000/contacts')
        const data = await req.json()
        this.contacts = data
      },
      
      async deleteBurger(id) {
        const req = await fetch(`http://localhost:3000/contacts/${id}`, {
          method: "DELETE"
        });
        const res = await req.json()
        this.getPedidos()
      },

      async updateBurger(id) {
        const dataJson = JSON.stringify()
        const req = await fetch(`http://localhost:3000/contacts/${id}`, {
          method: "PATCH",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });
        const res = await req.json()
        console.log(res)
      }
    },

    mounted () {
    this.getPedidos()
    }
  }
</script>


<style scoped>
  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }
  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
  }
  #burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }
  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }
  #burger-table-heading div,
  .burger-table-row div {
    width: 19%;
  }
  #burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }
  select {
    padding: 12px 6px;
    margin-right: 12px;
  }
  .delete-btn {
    background-color: red;
    color:#fff;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .delete-btn:hover {
    background-color: rgb(250, 68, 68);
    color: #222;
  }


  .edit-btn {
    background-color: rgb(135, 142, 151);
    color:#fff;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .edit-btn:hover {
    background-color: lightgrey;
    color: #222;
  }
  
</style>