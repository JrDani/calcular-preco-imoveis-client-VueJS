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
            
            <h1 class="text-left mt-2">Cadastrar imóvel</h1>

            <form @submit.prevent="adiciona()">
                <RegiaoComboBox v-on:bairro_selecionado="bairroSet($event)"></RegiaoComboBox>

                <div>
                    <label for="area">Area: </label>
                    <input type="text" id="area" v-model="area">
                </div>

                <div>
                    <label for="preco">Preco: </label>
                    <input type="text" id="preco" v-model="preco">
                </div>

                <div>
                    <label for="quartos">Quartos: </label>
                    <input type="text" id="quartos" v-model="quartos">
                </div>

                <div>
                    <label for="tipo">Tipo: </label>
                    <select v-model="tipo" id="tipo">
                        <option value="">Selecione o tipo</option>
                        <option v-for="t in tipos" :key="t.id" :value="t.id">{{ t.nome }}</option>
                    </select>
                </div>

                <input type="submit" value="Enviar" class="btn">

            </form>


        </main>

        <div class="assine">
            <p1-assine></p1-assine>
        </div>

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
import RegiaoComboBox from '../../form/RegiaoComboBox.vue';
import {v1} from '../../../apiUrls.js';
import axios from 'axios';

export default {        
    components:{
        'p1-menu': Menu,
        'p1-logo': Logo,
        'p1-feature' : Feature,
        'p1-assine' : Assine,
        'p1-footer' : Footer,
        'p1-chamada' : Chamada,
        RegiaoComboBox

    },
    data(){
        console.log(v1.tipos);
        return {            
            tipos: [],
            bairro: '',
            area: '',
            tipo: '',
            preco: '',
            quartos: ''

        }
    },
    methods:{
        loadTipos(){
            axios.get(v1.tipos)
            .then(response =>{               
                this.tipos = response.data;
            })
            .catch(error =>{
                console.log(error);
            })
        },
        bairroSet: function(value){
          this.bairro = value;
        },
        adiciona(){
            axios.post(v1.amostras,{
                area: this.area,
                quantidade_quartos: this.quartos,
                preco: this.preco,
                fk_vizinhanca: this.bairro,
                fk_tipo: this.tipo
            })
            .then(response=>{
                console.log(response.data);
            })
            .catch(error=>{
                console.log(error);
            })
            
        }
    },
    created(){
        this.loadTipos()
    }


}

</script>

<style>

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
    .features{
        display: grid;
        grid-gap: 10px;
        grid-template-columns: repeat(12, 1fr);  
        grid-template-areas: "l l l l m m m m r r r r";
    }
}

@media (min-width: 1440px) {
    .container{
        grid-template-columns: 1fr 1200px 1fr;
    }
}



</style>
