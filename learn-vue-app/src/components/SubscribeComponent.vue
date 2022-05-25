<template>
    <table border>
        <tr>
            <th>Firstname</th>
            <th>Lastname</th>
            <th>Age</th>
        </tr>
        <tr v-for="(people, index) in lists" :key="index">
            <td>{{people.firstname}}</td>
            <td>{{people.lastname}}</td>
            <td>{{people.age}}</td>
        </tr>
    </table>
</template>
<script>
export default {
    name: 'SubscribeComponent',
    props: ['lists']
}
</script>
<style>
    th {
        background: lightgrey;
        font-size: 140%;
    }
    td {
        width: 10rem;
        text-align: center;
    }
</style>