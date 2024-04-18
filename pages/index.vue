<template>
    <div class="main-container">
        <h1>To - Do</h1>
        <div class="list">
            <item v-for="(data, index) in listData" :key="index" :data="data" :handler="fetchData"/>
        </div>
        <h3 v-if="!(listData.length > 0)">Fetching data from api (please wait)...</h3>

        <input type="text" v-if="add" v-model="text"/>
        <div class="add" @click="addit" >Add</div>
        <div class="space"></div>

    </div>
</template>

<script setup>
import { ref } from 'vue';

let listData = ref([])
let add = ref(false)
let text = ref('')

const addit = async() =>{

    if (add.value && (text.value.length > 0)){
        console.log("added")
        add.value = !add.value; 
        const items = await addItem(text.value)
        text.value = ''
        fetchData()

    } else {
        add.value = !add.value; 
    }
}
const fetchData = async () => {
    try {
        const items = await getItems(); // Wait for getStacks to resolve
        console.log(items['Items'])
        listData.value = items['Items']
        listData.value.sort((a, b) => {
            // If a is not done and b is done, a comes before b
            if (!a.done && b.done) {
                return -1;
            }
            // If a is done and b is not done, b comes before a
            else if (a.done && !b.done) {
                return 1;
            }
            // Otherwise, maintain the current order
            else {
                return 0;
            }
        });

    } catch (error) {
        console.error('There was a problem with the fetch operation:', error);
    }
};
const getItems = async () => {
    let responseData = {};

    try {
        const response = await fetch('https://2nlzpxbzp3.execute-api.us-east-1.amazonaws.com/todos');

        if (!response.ok) {
            throw new Error('Network response was not ok');
        }

        responseData = await response.json();
        return responseData

    } catch (error) {
      console.error('There was a problem with the fetch operation:', error);
    }
    
    return responseData;
}

const addItem = async (text) => {
    const newItem = {
        todo: text,
        description: 'Description of the new todo item',
        done: false
    };

    try {
        const response = await fetch('https://2nlzpxbzp3.execute-api.us-east-1.amazonaws.com/todos', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(newItem)
        });

        if (!response.ok) {
            throw new Error('Failed to add new item');
        }

        console.log('New item added successfully');
    } catch (error) {
        console.error('There was a problem adding the new item:', error);
    }
};

fetchData()
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
    padding-top: 80px;
    padding-bottom: 60px;
    font-size: 24px;
    font-weight: 400;
}

h3{
    margin-bottom: 24px;
    letter-spacing: 1px;
}

input{
    width: 400px;
    height: 20px;
    padding: 10px;
    font-size: 24px;
    font-weight: 200;
    outline: none;
}
.add{
    min-width: 120px;
    min-height: 50px;
    margin-top: 10px;
    background-color: #000;
    color: #fff;
    letter-spacing: 4px;
    font-size: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    cursor: pointer;
}

.space{
    min-width: 200px;
    min-height: 100px;
}
</style>