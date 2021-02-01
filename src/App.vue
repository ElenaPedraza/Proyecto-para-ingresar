<template>
  <div id="app">
    <div id="navBar">
      <b-navbar type="dark" variant="info">
        <b-navbar-nav>
          <b-nav-item href="#">App People</b-nav-item>

          <!--
          <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">ES</b-dropdown-item>
            <b-dropdown-item href="#">RU</b-dropdown-item>
            <b-dropdown-item href="#">FA</b-dropdown-item>
          </b-nav-item-dropdown>

          <b-nav-item-dropdown text="User" right>
            <b-dropdown-item href="#">Account</b-dropdown-item>
            <b-dropdown-item href="#">Settings</b-dropdown-item>
          </b-nav-item-dropdown> -->
        </b-navbar-nav>
      </b-navbar>
    </div>
    <img alt="Vue logo" src="./assets/persona.png">
    <HelloWorld msg="Personas APP"/>
    <LoadingScreen :isLoading="isLoading" />



  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import LoadingScreen from './components/LoadingScreen.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    LoadingScreen
  },

}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
#navBar{
  margin-bottom: 5%;
}
</style>
