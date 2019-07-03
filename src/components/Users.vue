<template>
    <div id="users">
        <div class="container">
            <p v-if="loading">Loading...</p>
            <div v-else>
              <header class="head">
                <h1>Users</h1>
              </header>
                <table>
                    <tr>
                        <th>Id</th>
                        <th>Name</th>
                        <th>Username</th>
                        <th>Email</th>
                        <th>Address</th>
                        <th>Phone</th>
                        <th>Website</th>
                        <th>Company</th>
                        <th>Action</th>
                    </tr>
                    <tr v-for="(value, key) in post" :key="value.id">
                        <td>{{value.id}}</td>
                        <td>{{value.name}}</td>
                        <td>{{value.username}}</td>
                        <td>{{value.email}}</td>
                        <td><b>Street:</b> {{value.address.street}}<br>
                            <b>Suite:</b> {{value.address.suite}}<br>
                            <b>City:</b> {{value.address.city}}<br>
                            <b>Zipcode:</b> {{value.address.zipcode}}<br>
                            <b>Geo:</b> (lat: {{value.address.geo.lat}},lng {{value.address.geo.lng}})</td>
                        <td>{{value.phone}}</td>
                        <td>
                            <a v-bind:href="'https://'+value.website" target="_blank">{{value.website}}</a>
                        </td>
                        <td><b>Name:</b> {{value.company.name}}<br>
                            <b>Catch Phrase:</b> {{value.company.catchPhrase}}<br>
                            <b>Bs:</b> {{value.company.bs}}<br></td>
                        <td>
                            <div>
                                <button v-on:click="deleteData(value.id,key)">DELETE</button>
                            </div>
                        </td>
                    </tr>
                </table>
            </div>
            <p v-if="error">{{ error }}</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
require('@/assets/styles/table.css')
export default {
    name: 'Users',
    data() {
        return {
            loading: false,
            post: null,
        }
    },
    created: function() {
        this.loading = true
        axios
            .get('https://jsonplaceholder.typicode.com/users')
            .then(respond => {
                this.loading = false
                this.post = respond.data
            })
            .catch(err => {
                this.loading = false
                this.error = err
            })
    },
    methods: {
        deleteData(id, key) {
            axios
                .delete('https://jsonplaceholder.typicode.com/users/' + id, {
                    method: 'DELETE'
                })
                .then(res => {
                    this.post.splice(key, 1)
                })
            console.log(this.post)
        }
    }
}
</script>



