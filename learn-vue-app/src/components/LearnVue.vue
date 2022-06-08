<template>
    <div class="header">
        <div class="hour">
            <p>Heure FR: {{calculate_hour_fr}}</p>
            <p>Heure US: {{calculate_hour_us}}</p>
        </div>
        <div class="title">
            <h1>Subscribes list</h1>
        </div>
        <img :src="url"/>
    </div>
    <div class="main">
        <p>Click number on the button: {{nbClick}}</p>
        <button @click="nbClick += 1">Click on me!</button>
        <hr/>
        <fieldset>
            <legend>Choosen</legend>
            <select name="cities" v-model="cities" id="cities-select">
                <option>Paris</option>
                <option>Londres</option>
                <option>Madrid</option>
            </select>
            <p>Your choice: {{cities}}</p>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Writing</legend>
            <textarea v-model="multi" cols="40" rows="7"></textarea>
            <div style="white-space: pre-line;">{{multi}}</div>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Writing your name</legend>
            <input type="text" v-model="text1" v-on:keyup="copy"/>
            <input type="text" v-bind:value="text2"/>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Check the language you know</legend>
            <div class="input-checkbox">
                <input type="checkbox" v-model="languages" value="html"/>
                <label for="html">HTML</label>
                <input type="checkbox" v-model="languages" value="css"/>
                <label for="html">CSS</label>
                <input type="checkbox" v-model="languages" value="js"/>
                <label for="html">JavaScript</label>
                <p>Checkbox: {{languages}}</p>
            </div>
        </fieldset>
        <br/>
        <fieldset class="input-radio">
            <legend>What's your favorite language ?</legend>
            <div>
                <input type="radio" v-model="favorite" value="html"/>
                <label for="html">HTML</label>
            </div>
            <div>
                <input type="radio" v-model="favorite" value="css"/>
                <label for="html">CSS</label>
            </div>
            <div>
                <input type="radio" v-model="favorite" value="js"/>
                <label for="html">JavaScript</label>
            </div>
            <p>Favorite language: {{favorite}}</p>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Enter your name</legend>
            <input type="text" v-model="name"/>
            <button @click="hello('Hello')">Say 'Hello'</button>
            <button @click="hello('Bonjour')">Say 'Bonjour'</button>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Enjoy with this picture</legend>
            <img :src="url" @mousemove="hoverImg($event)"/>
            <div>{{xy}}</div>
        </fieldset>
        <br/>
        <fieldset>
            <legend>The events</legend>
            <div @keydown="actionParent">
                <input type="text" @keydown.prevent.stop="action($event)"/>
            </div>
            <p><a href="https://google.com" @click="stop($event)">Google</a></p>
            <p><a href="https://bing.com">Bing</a></p>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Updating</legend>
            <input type="text" v-model="text" @keyup.enter="update" autofocus/>
            <input type="button" value="uppercase" @click="update"/>
        </fieldset>
        <fieldset>
            <legend>Check the language you know</legend>
            <input type="text" v-model="valueCheck"/>
            <input type="button" value="Add" @click="add"/>
            <div v-for="(language, i) in languagesKnow" :key="i">
                <input type="checkbox" v-model="language.state"/>
                {{language.lang}}
                <span v-if="language.state">Is checked !</span>
                <span v-else>Is not checked !</span>
            </div>
        </fieldset>
        <SubscribeComponent :lists="peoples"></SubscribeComponent>
    </div>
</template>

<script>
import SubscribeComponent from './components/SubscribeComponent.vue';
export default {
	name: 'LearnVue',
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
			text1: '',
			text2: '',
			languages: [],
			favorite: '',
			nbClick: 0,
			name: '',
			xy: 0,
			lang: '',
			text: '',
			valueCheck: '',
			languagesKnow: [],
		}
	},
	computed: {
		calculate_hour_fr() {
		    return this.d.toLocaleTimeString()
		},
		calculate_hour_us() {
		    return this.d.toLocaleTimeString('en-US')
		}
	},
	methods: {
		copy() {
			this.text2 = this.text1.toUpperCase()
		},
		hello(type) {
			alert(type + ' ' + this.name);
		},
		hoverImg(ev) {
			this.xy = 'x = ' + ev.offsetX + ', y = ' + ev.offsetY
		},
		actionParent() {
			console.log('Event treated in the parent.');
		},
		action(ev) {
			console.log('Event treated in the input');
			ev.preventDefault();
			// ev.stopPropagation();
		},
		stop(ev) {
			ev.preventDefault();
		},
		update() {
			this.text = this.text.toUpperCase();
		},
		add() {
			this.languagesKnow.push({lang: this.valueCheck, state: false})
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
  .header {
    display: flex;
    justify-content: space-around;
  }
  img {width: 15%;}
  legend {font-weight: bold;}
</style>
