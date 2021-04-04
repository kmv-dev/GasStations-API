<template>
    <div v-for="station of stations" :key="station.id">
        <ul>
            <li>название {{ station.name }}</li>
            <li>Адрес {{ station.address }}</li>
        </ul>
    </div>
</template>

<script>
const axios = require('axios');
export default {
    name: 'About',
    data() {
        return {
            stations: [],
        }
    },
    mounted() {
        Promise.all([
            axios.get(`http://localhost:3000/stations`),
            axios.get(`http://localhost:3000/cars`)
        ]).then(([stations, cars]) => {
            this.stations = stations.data;
            this.cars = cars.data;
        });
    },
}
</script>
