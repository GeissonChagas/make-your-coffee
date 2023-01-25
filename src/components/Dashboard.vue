<template>
    <div id="coffee-table" v-if="coffees">
      <div>
        <div id="coffee-table-heading">
          <div class="order-id">#:</div>
          <div>Cliente:</div>
          <div>Pão:</div>
          <div>Carne:</div>
          <div>Opcionais:</div>
          <div>Ações:</div>
        </div>
      </div>
      <div id="coffee-table-rows">
        <div class="coffee-table-row" v-for="coffee in coffees" :key="coffee.id">
          <div class="order-number">{{ coffee.id }}</div>
          <div>{{ coffee.nome }}</div>
          <div>{{ coffee.tipocafe }}</div>
          <div>{{ coffee.origem }}</div>
          <div>
            <ul v-for="(opcional, index) in coffee.opcionais" :key="index">
              <li>{{ opcional }}</li>
            </ul>
          </div>
          <div>
            <select name="status" class="status" @change="updateCoffee($event, coffee.id)">
              <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="coffee.status == s.tipo">
                {{ s.tipo }}
              </option>
            </select>
            <button class="delete-btn" @click="deleteCoffee(coffee.id)">Cancelar</button>
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
      name: "Dashboard",
      data() {
        return {
          coffees: null,
          coffee_id: null,
          status: []
        }
      },
      methods: {
        async getPedidos() {
          const req = await fetch('http://localhost:3000/coffees')
          const data = await req.json()
          this.coffees = data
          // Resgata os status de pedidos
          this.getStatus()
        },
        async getStatus() {
          const req = await fetch('http://localhost:3000/status')
          const data = await req.json()
          this.status = data
        },
        async deleteCoffee(id) {
          const req = await fetch(`http://localhost:3000/coffees/${id}`, {
            method: "DELETE"
          });
          const res = await req.json()
          this.getPedidos()
        },
        async updateCoffee(event, id) {
          const option = event.target.value;
          const dataJson = JSON.stringify({status: option});
          const req = await fetch(`http://localhost:3000/coffees/${id}`, {
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
    #coffee-table {
      max-width: 1200px;
      margin: 0 auto;
    }
    #coffee-table-heading,
    #coffee-table-rows,
    .coffee-table-row {
      display: flex;
      flex-wrap: wrap;
    }
    #coffee-table-heading {
      font-weight: bold;
      padding: 12px;
      border-bottom: 3px solid #333;
    }
    .coffee-table-row {
      width: 100%;
      padding: 12px;
      border-bottom: 1px solid #CCC;
    }
    #coffee-table-heading div,
    .coffee-table-row div {
      width: 19%;
    }
    #coffee-table-heading .order-id,
    .coffee-table-row .order-number {
      width: 5%;
    }
    select {
      padding: 12px 6px;
      margin-right: 12px;
    }
    .delete-btn {
      background-color: #222;
      color:#fcba03;
      font-weight: bold;
      border: 2px solid #222;
      padding: 10px;
      font-size: 16px;
      margin: 0 auto;
      cursor: pointer;
      transition: .5s;
    }
    
    .delete-btn:hover {
      background-color: transparent;
      color: #222;
    }
    
  </style>