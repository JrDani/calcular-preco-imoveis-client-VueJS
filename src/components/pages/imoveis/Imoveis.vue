<template>
    <div class="container">  
       
        <div class="header">
            <div class="logo">
                <p1-logo></p1-logo>
            </div>
            <div class="menu">
                <p1-menu></p1-menu>
            </div>
        </div>       

        <main>
            
            <div>
                <h1 class="text-left">Imóveis cadastrados no sistema</h1>
                <table class="tabela">
                    <thead>     
                        <td>Região</td>
                        <td>Área m²</td>
                        <td>Valor R$</td>
                        <td>Nº Quartos</td>
                        <td>Tipo</td>                  
                    </thead>
                    <tr v-for="todo in todos" :key="todo.id"> 
                        <td>{{ todo.regiao }}</td>
                        <td>{{ todo.area }}</td>
                        <td>{{ todo.preco }}</td>
                        <td>{{ todo.quartos }}</td>
                        <td>{{ todo.tipo }}</td>
                    </tr>
                </table>
               
            </div>

            <div class="assine">
                <p1-assine></p1-assine>
            </div>

        </main>

        <footer>
            <p1-footer></p1-footer>
        </footer>
         
    </div> 
</template>

<script>
import Menu from '../../header/menu/Menu.vue';
import Logo from '../../header/logo/Logo.vue';
import Feature from '../../main/feature/Feature.vue';
import Assine from '../../main/assine/Assine.vue';
import Footer from '../../footer/footer/Footer.vue';
import Chamada from '../../header/chamada/Chamada.vue';
import axios from 'axios';

export default {    
    components:{
        'p1-menu': Menu,
        'p1-logo': Logo,
        'p1-feature' : Feature,
        'p1-assine' : Assine,
        'p1-footer' : Footer,
        'p1-chamada' : Chamada
    },
    data(){
        return {
            todos: []
        }
    },
    methods: {
      create() {
        // To do
      },
      read() {
        axios.get('http://localhost:8000/api/v1/imoveis')
        .then(response => {
            this.todos = response.data
        })
        .catch(error => {
            console.log(error);
        })
      },
      update(id, color) {
        // To do
      },
      del(id) {
        // To do
      }
    },
    created() {
        this.read()
    }
}

</script>

<style>
.tabela{
    width: 100%;
    margin-top: 30px
}
.tabela tr{
    line-height: 2em;
}
thead{
    font-weight: bold
}

.container{
    width: 100%;
    min-height: 100%;
    display: grid;
    grid-template-columns: 20px 1fr 20px;
    padding-top: 80px;
}

.container > div, .container > *{
  grid-column: 2;
  min-width: 0
}

.header{
    width: 100%;
    position: fixed;
    display: grid;
    grid-template-columns: 1fr 1fr;    
    padding:20px 0;
    grid-template-areas: "logo menu";
    max-height: 100%;
    overflow-y: auto
}

.logo{
    grid-area: logo;   
}

.logo a{
    width: 100%;    
}

.menu{
    grid-area: menu;   
    position: relative;    
}
.assine_left{
    width: 100%;
    height: auto;   
    box-sizing: border-box;
}

.assine_left ul li{
    display: inline-block
}

.assine_right{
    width: 100%;
    height: auto;   
    box-sizing: border-box;
}
@media (min-width: 600px) {
    .container{
        grid-template-columns: 40px 1fr 40px;
        padding-top: 0;
    }
    
    .header{
        text-align: left;
        position:static;
        display:initial;
        padding:40px 0 !important;
        overflow: hidden;
    }

    .logo{
        display: initial;
        width: 50%;
        position:absolute;
        left: 0;
        padding-left: 40px;
        box-sizing: border-box
    }

    
}

@media (min-width: 900px) {
    .container{
        grid-template-columns: 120px 1fr 120px;
       
    }
    .header{
        display: grid;
        grid-template-columns: repeat(12, 1fr);
        margin-top: 50px;
    }
    .menu{
        position: static;
        grid-column:  4 / 12 ;
        grid-auto-rows: 24px 24px;
    }
    .logo{
        grid-column: 1 / 3;
        position: initial;
        padding-left: 0;
        width: 100%;  
    }
}

@media (min-width: 1440px) {
    .container{
        grid-template-columns: 1fr 1200px 1fr;
    }
}



</style>
