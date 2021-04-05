<template>
    <div class="wrap main">
        <div class="main__item" v-for="{ sum, station, cars } in stationsWithCars" :key="station.id">
            <h1><i class="fas fa-gas-pump"></i> {{ station.name }}</h1>
            <ul>
                <li>Заправилось <span>{{ cars.length }} </span> автомобиля</li>
                <li>На общее количество <span>{{ sum }}</span> Л</li>
            </ul>
        </div>
        <h2>Общее количество заправленного топлива = {{ carsSumGas }}л </h2>
    </div>
</template>

<script>

const axios = require('axios');

export default {
    name: 'Home',
    data() {
        return {
            stations: [],
            cars: [],
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
    computed: {
        stationsWithCars() {
            return this.cars.reduce(
                (acc, n) => {
                    const item = acc[n.address];
                    if (item) {
                        item.cars.push(n);
                        item.sum += +n.count;
                    }

                    return acc;
                },
                Object.fromEntries(this.stations.map(n => [
                    n.name,
                    {
                        station: n,
                        cars: [],
                        sum: 0,
                    }
                ]))
            );
        },
        carsSumGas() {
            return this.cars.reduce((s, i) => s = s + +i.count, 0)
        }
    },
}
</script>
