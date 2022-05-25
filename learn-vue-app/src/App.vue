<template>
	<div id="app" class="app">
		<h1>Subscribes list</h1>
    <img :src="url"/>
    <p>Heure FR: {{calculate_hour_fr}}</p>
    <p>Heure US: {{calculate_hour_us}}</p>
    <p>You choose: {{cities}}</p>
    <select name="cities" v-model="cities" id="cities-select">
      <option>Paris</option>
      <option>Londres</option>
      <option>Madrid</option>
    </select>
    <br/>
    <textarea v-model="multi" cols="40" rows="7"></textarea>
    <div style="white-space: pre-line;">{{multi}}</div>
    <SubscribeComponent :lists="peoples"></SubscribeComponent>
	</div>
</template>

<script>
import SubscribeComponent from './components/SubscribeComponent.vue';
export default {
  name: 'App',
  components: {SubscribeComponent},
  data() {
    return {
      peoples: [
        {'firstname': 'Jean', 'lastname': 'Bréhat', age: 20},
        {'firstname': 'Léa', 'lastname': 'Prijean', age: 25},
        {'firstname': 'Chris', 'lastname': 'Martin', age: 38},
        {'firstname': 'Pierre', 'lastname': 'Petit', age: 18},
      ],
      d: new Date(),
      url: 'https://vuejs.org/images/logo.png',
      cities: '',
      multi: '',
    }
  },
  computed: {
    calculate_hour_fr() {
      return this.d.toLocaleTimeString()
    },
    calculate_hour_us() {
      return this.d.toLocaleTimeString('en-US')
    }
  }
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

</style>
