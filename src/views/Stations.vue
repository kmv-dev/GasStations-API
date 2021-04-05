<template>
    <div class="wrap">
        <div class="stations">
            <ul v-for="station of stations" :key="station.id" class="stations__item">
                <li><i class="fas fa-gas-pump"></i>АЗС - {{ station.name }}</li>
                <li><i class="fas fa-map-marker-alt"></i>Адрес - {{ station.address }}</li>
            </ul>
        </div>
        <form class="stations__form" @submit="addStations">
            <label>Название</label>
            <input type="text" v-model="stationName">
            <label>Адрес</label>
            <input type="text" v-model="stationAddress">
            <button type="submit">Добавить АЗС</button>
        </form>
    </div>
</template>

<script>
const axios = require('axios');
export default {
    name: 'Stations',
    data() {
        return {
            stations: [],
            stationName: '',
            stationAddress: '',
        }
    },
    mounted() {
        Promise.all([
            axios.get(`http://localhost:3000/stations`),
        ]).then(([stations]) => {
            this.stations = stations.data;
        });
    },
    methods: {
        addStations() {
            axios.post(`http://localhost:3000/stations`, {
                name: this.stationName,
                address: this.stationAddress
            })
        }
    }
}
</script>
