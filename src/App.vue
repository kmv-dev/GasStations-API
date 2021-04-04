<template>
    <div id="nav">
        <router-link class="r-link" to="/">Главная</router-link>
        |
        <router-link class="r-link" to="/stations">АЗС</router-link>
        |
        <router-link class="r-link" to="/cars">Автомобили</router-link>
    </div>
    <router-view/>
</template>

<style lang="scss" src="./scss/main.scss">

</style>
