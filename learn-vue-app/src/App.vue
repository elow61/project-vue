<template>
	<div id="app" class="app">
		<SearchPeople></SearchPeople>
	</div>
</template>

<script>
import SearchPeople from './components/SearchPeople.vue';
export default {
	name: 'App',
	components: {SearchPeople},
	data() {
		return {}
	},
}
</script>

<style>
  #app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
  }
</style>
