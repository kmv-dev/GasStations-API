<template>
    <div v-for="car of cars" :key="car.id">
        <ul>
            <li>Марка {{ car.name }}</li>
            <li>Номер {{ car.number }}</li>
            <li>Сколько заправляет {{ car.count }}</li>
            <li>Где заправляет {{ car.address }}</li>
        </ul>
    </div>
</template>

<script>
const axios = require('axios');
export default {
    name: 'About',
    data() {
        return {
            cars: [],
        }
    },
    mounted() {
        Promise.all([
            axios.get(`http://localhost:3000/cars`)
        ]).then(([cars]) => {
            this.cars = cars.data;
        });
    },
}
</script>
