<template>
    <div class="assine-box">
        <div class="assine_left">
            <div>
                <h3>lorem ipsum. go to pro plan</h3>
                <ul>
                    <li><a href="">unlimited</a></li> |
                    <li><a href="">24/7</a></li> |
                    <li><a href="">free taxes</a></li> | 
                    <li><a href="">free whatever</a></li>                 
                </ul>
            </div>
        </div>
        <div class="assine_right">
            <div>    
             Planos começam com $25/month
            </div> 
            <div> 
                <a href="" class="btn">Assine</a>    
            </div>             
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
.assine_left{
    padding: 20px 30px;
}
.assine_left h3{
    font-family: 'Times New Roman', Times, serif;
    text-transform: uppercase;
    margin-bottom: .5em;   
}

.assine_left a{
    text-decoration: underline
}
.assine_right{
    padding: 20px 30px;
}

.assine_right div:first-of-type{
    margin-bottom: 10px
}

@media (min-width: 600px) {
    .assine-box{
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        grid-template-rows: 100px;
        grid-template-areas: "l l l r r";
    }
    .assine_left{
        grid-area: l;
        padding: 0;
        display: grid;
        align-items: center
    }   

    .assine_left > div{
       grid-column: 1;
    }
   
    .assine_right{
        grid-area: r;   
        padding: 0 10px;
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 100px;
        align-items: center
        
    }
    .assine_right div:first-child{
        grid-row: 1;   
    }
    .assine_right div:last-child{    
        grid-row: 1;   
        grid-column: 1;        
    }

}
@media (min-width: 900px) {
    .assine_right{
        grid-template-columns: 1fr 2fr;
        text-align: left;
    }
    .assine_right div:first-child{
        grid-column: 2/3;    
        justify-self: left
    }
    .assine_right div:last-child{    
        grid-column: 1/2;        
    }
}
</style>
