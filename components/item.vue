<template>
    <div class="item-container" @click="toggle">
        <h2>{{ data.todo }}</h2>
        <div class="checkbox">
            <img src="../images/check.png" alt="" v-if="data.done">
        </div>
        <div class="done" v-if="data.done"></div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    data: Object,
    handler: Function
})

const toggleCompletion = async (item) => {
    
    try {
        const response = await fetch('https://2nlzpxbzp3.execute-api.us-east-1.amazonaws.com/toggle', {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(item)
        });
        
        if (!response.ok) {
            throw new Error('Failed to toggle item');
        }
        
        console.log('toggled successfully');
    } catch (error) {
        console.error('There was a problem toggling the item:', error);
    }
};

const toggle = async() =>{
    const dataToSend = props.data
    await toggleCompletion(dataToSend);
    props.handler();
}
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
    margin-bottom: 24px;
    animation: slide 0.3s;
}

.item-container h2{
    font-size: 24px;
    font-weight: 500;
    max-width: 400px;
    margin-left: 40px;
    
}
.checkbox{
    width: 20px;
    height: 20px;
    border: 2px solid #000;
    margin-right: 25px;
    position: relative;
}

.checkbox img{
    position: absolute;
    bottom: -2px;
    left: -2px;
    width: 24px;
    height: auto;
}

.done{
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
    background-color: #00000023;
}


@keyframes slide {
    0% {
        opacity: 0;
        transform: translateX(-20px);
    }
    80% {
        transform: translateX(10px);
    }
    100% {
        opacity: 1;
        transform: translateX(0);
    }
}
</style>