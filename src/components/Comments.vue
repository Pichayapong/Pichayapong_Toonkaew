<template>
    <div id="comments">
        <div class="container">
            <p v-if="loading">Loading...</p>
            <div v-else>
              <header class="head">
                <h1>Comments</h1>
              </header>
                <table>
                    <tr>
                        <th>Post Id</th>
                        <th>Id</th>
                        <th>name</th>
                        <th>Email</th>
                        <th>Body</th>
                        <th>Action</th>
                    </tr>
                    <tr v-for="(value, key) in post" :key="value.id">
                        <td>{{value.postId}}</td>
                        <td>{{value.id}}</td>
                        <td>{{value.name}}</td>
                        <td>{{value.email}}</td>
                        <td>{{value.body}}</td>
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
    name: 'Comments',
    data() {
        return {
            loading: false,
            post: null,
        }
    },
    created: function() {
        this.loading = true
        axios
            .get('https://jsonplaceholder.typicode.com/comments')
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
                .delete('https://jsonplaceholder.typicode.com/comments/' + id, {
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



