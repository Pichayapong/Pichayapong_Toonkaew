<template>
    <div id="photos">
        <div class="container">
            <p v-if="loading">Loading...</p>
            <div v-else>
              <header class="head">
                <h1>Photos</h1>
              </header>
                <table>
                    <tr>
                        <th>Album Id</th>
                        <th>Id</th>
                        <th>Url</th>
                        <th>Thumnail Url</th>
                        <th>Action</th>
                    </tr>
                    <tr v-for="(value, key) in post" :key="value.id">
                        <td>{{value.albumId}}</td>
                        <td>{{value.id}}</td>
                        <td>
                            <a v-bind:href="value.url">{{value.url}}</a>
                        </td>
                        <td>
                            <img :src="value.thumbnailUrl" />
                        </td>
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
    name: 'Photos',
    data() {
        return {
            loading: false,
            post: null,
        }
    },
    created: function() {
        this.loading = true
        axios
            .get('https://jsonplaceholder.typicode.com/photos')
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
                .delete('https://jsonplaceholder.typicode.com/photos/' + id, {
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



