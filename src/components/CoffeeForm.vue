<template>
    <div>
        <p>Componente de mensagem</p>
        <div>
            <form id="coffee-form" @submit="createCoffee">
                <div class="input-container">
                    <label for="name">Nome e sobrenome:</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Digite seu nome e sobrenome.">
                </div>
                <div class="input-container">
                  <label for="tipocafe">Escolha o tipo de café:</label>
                    <select name="tipocafe" id="tipocafe" v-model="tipocafe">
                      <option value="">Selecione o tipo de café</option>
                      <option v-for="tipocafe in tipocafes" :key="tipocafe.id" :value="tipocafe.tipo">{{ tipocafe.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="origem">Escolha a origem do café</label>
                    <select id="origem-cafe" name="origem-cafe" v-model="origem">
                        <option value="">Selecione a origem do seu café</option>
                        <option v-for="origem in origens" :key="origem.id" :value="origem.tipo">{{ origem.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="origem">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                          <span>{{ opcional.tipo }}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" name="submit" id="submit" class="submit-btn" value="Enviar pedido">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        name: "CoffeeForm",
        data () {
          return{
            tipocafe: null,
            origem: null,
            opcionaisdata: null,
            nome: null,
            tipocafes: null,
            opcionais: [],
            status: "Solicitado",
            msg: null,
          }
        },
        methods: {
          async getIngredientes(){
            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();

            this.tipocafes = data.tipocafes;
            this.origens = data.origens;
            this.opcionaisdata = data.opcionais;
            
          }
        },
        mounted () {
          this.getIngredientes();
        }
    } 

    


</script>

<style scoped>
  #coffee-form {
    max-width: 400px;
    margin: 0 auto;
  }
  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #582900;
  }
  input, select {
    padding: 5px 10px;
    width: 100%;
    border: 1px solid #582900;
    border-radius: 8px;
  }
  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }
  #opcionais-title {
    width: 100%;
  }
  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }
  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }
  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }
  .submit-btn {
    background-color: #222;
    color:#a06c3f;
    font-weight: bold;
    border: 2px solid #222;
    border-radius: 8px;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>