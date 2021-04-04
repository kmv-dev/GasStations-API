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
    name: 'Stations',
    data() {
        return {
            stations: [],
        }
    },
    mounted() {
        Promise.all([
            axios.get(`http://localhost:3000/stations`),
        ]).then(([stations]) => {
            this.stations = stations.data;
        });
    },
}
</script>
