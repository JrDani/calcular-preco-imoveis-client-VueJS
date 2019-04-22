<template>
    <div class="content">
        
        <div class="content_title">
          <h2>Lorem ipsum dolor </h2>
        </div>

        <div class="content_image">
            <div class="img-placeholder img-placeholder-g"></div>
        </div>

        <div class="content_text">
            <p>Duis pretium est et purus varius feugiat. 
                Quisque volutpat vitae est ut euismod. 
                Cras eu consectetur massa. Vestibulum dignissim tempor risus ac convallis. 
                Fusce ultrices convallis pretium. 
                Mauris nec purus nec ipsum iaculis pellentesque eget eu augue.
                Suspendisse vitae velit id nisl elementum congue.
                Nulla nec orci egestas, aliquet mi non, dapibus felis.
                Fusce venenatis et ex non sodales.
                Morbi porta tincidunt quam
                <a href="" class="details text-left">More details</a>
            </p>
        </div>
        
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
@media (min-width: 1140px) {
    .content{
        display: grid;
        grid-template-columns: repeat(12, 1fr);
        grid-template-areas: 
        ". t t t t t . . . . . ."
        ". c c c c c . i i i i i";
        grid-template-rows: 24px 1fr ;
    }
    h2, p, .details{
        text-align: right !important
    }
    .content_title{
        grid-area: t;
    }
    .content_image{
        grid-area: i;        
    }
    .content_text{
        grid-area: c;
    }
    .img-placeholder{
        margin-left: 0
    }
    .details{
        display: block;
    }
}
</style>

