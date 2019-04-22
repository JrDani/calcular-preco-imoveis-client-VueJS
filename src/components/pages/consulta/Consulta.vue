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
                <h1 class="text-left">Consulte um preço</h1>
                
                <form v-if="form" action="" class="consulta-form" @submit="submitConsulta($event)">
                   
                    <RegiaoComboBox v-on:bairro_selecionado="bairroSet($event)"></RegiaoComboBox>

                    <div>
                        <label for="area">Área m²:</label>                             
                        <input type="text" id="area" v-model="area" placeholder="Ex: 100.50" >
                    </div> 

                    <div>
                        <label for="quartos">Número de quartos:</label>                             
                        <input type="text" id="quartos" v-model="quartos">
                    </div>

                    <div>
                        <label for="tipo">Tipo de imóvel:</label>                             
                        <select v-model="tipo" id="tipo" >       
                            <option value="">Selecione um tipo</option>                   
                            <option v-for="t in select_tipo" :key="t.id" :value="t.id">{{ t.nome }}</option>
                        </select> 
                    </div>

                    <input type="submit" class="btn" value="Enviar">
                </form>

                <div v-if="div_resultado">
                    <div>
                        Preço por m² na região: {{ formatPrice(resultado.valor_area) }}<br /><br/>
                        O preço do seu imóvel sem depreciação é 
                        <strong>
                            {{ formatPrice(resultado.valor_area * area)}}
                        </strong>                    
                    </div>

                    <div class="mt-2">
                        <a href="/#/consulta" class="btn" @click="refaz()">Voltar para consulta</a>
                    </div>
                </div>
               
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
import RegiaoComboBox from '../../form/RegiaoComboBox.vue';
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
        return {
            form: true,
            div_resultado: false,     
            select_tipo: [],     
            
            area: '',
            quartos: '',
            tipo:'', 

            bairro: '',   

            resultado: ''
        }
    },
    methods: {     
      
      lerTipos(){
          axios.get('http://localhost:8000/api/v1/tipos')
          .then(response => {
              this.select_tipo = response.data;              
          })
          .catch(error => {
              console.log(error);
          })
      },
      bairroSet: function(value){
          this.bairro = value;
      },
      
      submitConsulta($event){
        event.preventDefault();                        
        let url = '?bairro='+this.bairro+'&area='+this.area+'&quartos='+this.quartos+'&tipo='+tipo;
        console.log(url);   
        axios
        .get('http://localhost:8000/api/v1/consultas'+url)
        .then(response => {
            this.form = false;
            this.div_resultado=true;
            this.resultado = response.data;
        })
        .catch(function (error) {
          console.log(error);
        })       
      },
      formatPrice(value) {
        let val = (value/1).toFixed(2).replace('.', ',')
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
      },
      refaz(){
          this.div_resultado = false;
          this.form = true;
      }
    },
    created() {
        this.lerTipos();
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

    .img-placeholder-g{
        width: 80%;
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
