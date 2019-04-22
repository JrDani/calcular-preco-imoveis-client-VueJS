<template>
    <div class="chamada">
        <div class="chamada_imagem">
            <div class="img-placeholder img-placeholder-m"></div>
        </div>

        <div class="chamada_content">
            <p>Proin sit amet odio vitae orci convallis dictum.                 
                Nam et lectus commodo, 
                dapibus massa sit amet, pretium nulla. 
                Vestibulum vel semper felis.
                Maecenas finibus convallis tortor, 
                id auctor felis faucibus in. Cras pulvinar, 
                nisi eu tristique ullamcorper.
            </p>
            <a href="" class="btn">learn more</a>
        </div>

        <div class="chamada_picture">
            <div class="img-placeholder img-placeholder-m"></div>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
.chamada p{
    margin-top: 0
}

.chamada_picture{
    display: none;
}


@media (min-width: 600px) {
    .chamada{
        display: grid;
        grid-gap: 20px;
        grid-template-columns: 20px 1fr 1fr 20px;
    }
    .chamada_imagem{       
        grid-column: 2;
    }

    .chamada_content{
        grid-column: 3;
    }
}
@media (min-width: 1140px) {
    .chamada_picture{
        display:initial;
    }
    .chamada{        
        grid-template-columns: repeat(12, 1fr);
        grid-gap: 20px;
        grid-template-areas: "l l l l m m m m r r r r";
    }
    .chamada_imagem{       
        grid-area: l;   
        justify-self: right;     
    }
    .chamada_content{
        grid-area: m;
    }
    .chamada_picture{
        grid-area: r;
    }
}
</style>
