<template>
    <ul>
        <li><a href="">16</a></li>
        <li><a href="">78</a></li>
        <li><a href="">14</a></li>
        <li><a href="">11</a></li>
    </ul>
</template>

<script>
export default {
    
}
</script>

<style scoped>
 ul li{
    display: inline-block
}
@media (min-width: 600px) {
    ul{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 50px 50px;
    }

}
</style>

