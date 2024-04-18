<template>
    <div class="item-container">
        <h2>Say hello</h2>
        <div class="checkbox">

        </div>
    </div>
</template>

<script setup>

</script>

<style lang="css" scoped>
.item-container{
    min-width: 460px;
    min-height: 70px;
    border: 2px solid #000;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.item-container h2{
    font-size: 24px;
    font-weight: 500;
    margin-left: 40px;
    
}
.checkbox{
    width: 20px;
    height: 20px;
    border: 2px solid #000;
    margin-right: 25px;
}
</style>