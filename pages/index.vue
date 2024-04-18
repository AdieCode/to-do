<template>
    <div class="main-container">
        <h1>To - Do</h1>
        <dv class="list">
            <item/>
        </dv>

        <div class="add">Add</div>

    </div>
</template>

<script setup>
import { ref } from 'vue';

const fetchData = async () => {
    try {
        const stacks = await getStacks(); // Wait for getStacks to resolve

    } catch (error) {
        console.error('There was a problem with the fetch operation:', error);
    }
};
const getStacks = async () => {
    let responseData = {};

    try {
        const response = await fetch('https://personal-buget-manager-api-part-2.onrender.com/stacks');

        if (!response.ok) {
            throw new Error('Network response was not ok');
        }

        responseData = await response.json();

    } catch (error) {
      console.error('There was a problem with the fetch operation:', error);
    }
    
    return responseData;
}
</script>


<style lang="css">
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

*{
    padding: 0;
    margin: 0;
}

body{
    font-family: "Roboto";
    letter-spacing: 4px;
    font-optical-sizing: auto;
    font-style: normal;
    color: #000;
    background-color: #fff;
}
</style>

<style lang="css" scoped>
.main-container{
    width: 100%;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

h1{
    padding-top: 160px;
    padding-bottom: 60px;
    font-size: 24px;
    font-weight: 400;
}

/* .list{

} */

.add{
    min-width: 120px;
    min-height: 50px;
    margin-top: 24px;
    background-color: #000;
    color: #fff;
    letter-spacing: 4px;
    font-size: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>