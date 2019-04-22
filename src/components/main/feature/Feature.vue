<template>
    <div class="feature-box">
        <div class="feature-img">
            <img v-bind:src="src" alt="">
        </div>
        <div class="feature-content">
            <h3>{{ titulo }}</h3>
            <p>{{ texto}}</p>
            <a href="" class="btn">more</a>      
        </div>  
    </div>
</template>

<script>
export default {
    props:['src', 'titulo', 'texto']
}
</script>

<style scoped>

h3{
    margin: 1em 0
}

@media (min-width: 600px) {
    .feature-box{
        display: grid;
        grid-column-gap: 20px;
        grid-template-columns: repeat(6, 1fr);   
        grid-template-areas: ". img c c c ."; 
    } 
    .feature-img{
        grid-area: img;
    }
    .feature-content{
        grid-area: c;
        text-align: left;        
    }
    .feature-content h3{
        text-align: left !important;   
    }
    .invert{
        grid-template-areas: ". c c c img ."; 
    }
    .invert h3, .invert p, .invert .feature-content {
        text-align: right !important;
    }
    h3{
        margin: .5em 0
    }
}

@media (min-width: 900px){
    .feature-box{       
        position: relative; 
        grid-template-columns: 10px 1fr 10px;  
        grid-template-areas: 
        ". img ."
        ". c ."; 
    }    
    .feature-content, .invert h3, .invert p, .invert .feature-content {  
        text-align: left !important;        
    }
    .invert{
      grid-template-areas: 
        ". img ."
        ". c .";
    }
    .feature-img{
        text-align: left;
    }

    h3{
        position: absolute;
        top: 12px;
        line-height: 24px;      
        left: 105px; 
        /* left: 10px margin left + 20px grid gap + 60 image width + 15 spaccing*/
        text-align: left
    }
}
</style>