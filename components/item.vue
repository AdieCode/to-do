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
    cursor: pointer;
    position: relative;
}

.item-container::after {
    content: ''; /* Add this line to create a pseudo-element */
    position: absolute;
    top: 0;
    left: 0;
    width: 0;
    height: 100%; /* Adjusted height */
    background-color: rgba(0, 0, 0, 0.10);
    transition: width 0.2s ease; /* Simplified transition property */
    z-index: -1; /* Added z-index to position the pseudo-element behind the content */
}

.item-container:hover::after {
    width: 100%; 
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