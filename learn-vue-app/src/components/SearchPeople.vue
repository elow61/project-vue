<script>
import people from '../assets/people.json';
export default {
    name: 'SearchPeople',
    data() {
        return {
            peoples: people,
            male: true,
            female: true,
            phone: true,
            picture_sizes: 'large',
            formatting: false,
            filterPeople: '',
        }
    },
}
</script>

<template>
    <form name="filter_people">
        <fieldset>
            <legend>Filter on the name</legend>
            <input type="text" name="name" v-model="filterPeople"/>
        </fieldset>
        <br/>
        <fieldset>
            <legend>Options</legend>
            <div>
                <label for="man">Man</label>
                <input type="checkbox" name="male" class="m-15" checked="checked" v-model="male"/>

                <label for="woman">Woman</label>
                <input type="checkbox" name="female" class="m-15" checked="checked" v-model="female"/>

                <label for="phone">Mobile</label>
                <input type="checkbox" name="phone" class="m-15" checked="checked" v-model="phone"/>

                <label for="picture_sizes">Picture</label>
                <select name="picture-sizes" v-model="picture_sizes" class="m-15" autocomplete="off">
                    <option selected="selected" value="large">Big</option>
                    <option value="medium">Medium</option>
                    <option value="thumbnail">Little</option>
                </select>

                <label for="formatting">Formatting</label>
                <input type="checkbox" name="formatting" v-model="formatting" class="input-option"/>
            </div>
        </fieldset>
    </form>
    <div class="main d-flex-column">
        <div v-for="(people, i) in peoples" :key="i">
            <div v-if="((male && people.gender === 'male') || (female && people.gender === 'female') && (people.name.last.indexOf(filterPeople) >= 0) || (filterPeople == ''))" :class="{format: formatting}" class="d-flex mb-15">
                <img :src="people.picture[picture_sizes]"/>
                <div class="ml-15">
                    <p>{{people.name.title}} {{people.name.first}} {{people.name.last}}</p>
                    <p v-if="phone">Phone: {{people.phone}}</p>
                    <p>Country: {{people.location.country}}</p>
                </div>
            </div>
        </div>
    </div>
</template>
<style>
    .ml-15 {margin-left: 15px;}
    .mb-15 {margin-bottom: 15px;}
    .m-15 {margin: 15px;}
    .d-flex {display: flex !important;}
    .d-flex-column {display: flex; flex-direction: column;}

    .main {margin-top: 20px;}
    .format {
        background-color: rgb(142, 182, 211);
        font-family: Georgia, 'Times New Roman', Times, serif;
        font-size: 1.2rem;
    }
</style>
