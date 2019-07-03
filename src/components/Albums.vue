<template>
    <div id="albums">
        <div class="container">
            <p v-if="loading">Loading...</p>
            <div v-else>
              <header class="head">
                <h1>Albums</h1>
              </header>
                <table>
                    <tr>
                        <th>User Id</th>
                        <th>Id</th>
                        <th>Title</th>
                        <th>Action</th>
                    </tr>
                    <tr v-for="(value, key) in post" :key="value.id">
                        <td>{{value.userId}}</td>
                        <td>{{value.id}}</td>
                        <td>{{value.title}}</td>
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
    name: 'Albums',
    data() {
        return {
            loading: false,
            post: null,
        }
    },
    created: function() {
        this.loading = true
        axios
            .get('https://jsonplaceholder.typicode.com/albums')
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
                .delete('https://jsonplaceholder.typicode.com/albums/' + id, {
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



