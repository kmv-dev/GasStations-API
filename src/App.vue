<template>
    <div id="nav" class="head">
        <router-link class="r-link head__link" to="/">Главная</router-link>
        |
        <router-link class="r-link head__link" to="/stations">АЗС</router-link>
        |
        <router-link class="r-link head__link" to="/cars">Автомобили</router-link>
    </div>
    <router-view/>
</template>

<style lang="scss" src="./scss/main.scss">

</style>
