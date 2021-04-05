<template>
    <div class="wrap cars">
        <ul class="cars__item" v-for="car of cars" :key="car.id">
            <li><i class="fas fa-car-side"></i> : {{ car.name }}</li>
            <li><i class="fas fa-arrow-alt-circle-right"></i> : {{ car.number }}</li>
            <li><i class="fas fa-gas-pump"></i> : {{ car.count }}л</li>
            <li><i class="fas fa-map-marked-alt"></i> : {{ car.address }}</li>
        </ul>
        <form class="cars__form" @submit="addStations">
            <label>Марка авто</label>
            <input type="text" v-model="carName">
            <label>Номер</label>
            <input type="text" v-model="carNumber">
            <label>Количество заправляемого топлива</label>
            <input type="number" v-model="carCount">
            <select v-model="carAddress">
                <option disabled value="">На какой АЗС заправляется</option>
                <option v-for="station of stations" :key="station.id">{{ station.name }}</option>
            </select>
            <button type="submit">Добавить авто</button>
        </form>
    </div>
</template>

<script>
const axios = require('axios');
export default {
    name: 'About',
    data() {
        return {
            cars: [],
            stations: [],
            carName: '',
            carNumber: '',
            carCount: '',
            carAddress: '',

        }
    },
    mounted() {
        Promise.all([
            axios.get(`http://localhost:3000/cars`),
            axios.get(`http://localhost:3000/stations`),
        ]).then(([cars, stations]) => {
            this.cars = cars.data;
            this.stations = stations.data;
        });
    },
    methods: {
        addStations() {
            axios.post(`http://localhost:3000/cars`, {
                name: this.carName,
                number: this.carNumber,
                count: this.carCount,
                address: this.carAddress
            })
        }
    }
}
</script>
