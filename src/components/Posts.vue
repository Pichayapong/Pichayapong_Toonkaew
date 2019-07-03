<template>
    <div id="todos">
        <div class="container">
            <p v-if="loading">Loading...</p>
            <div v-else>
                <h1>{{searchId}}</h1>
                <table>
                    <tr>
                        <th>User Id</th>
                        <th>Id</th>
                        <th>Title</th>
                        <th>Body</th>
                        <th>Action</th>
                    </tr>
                    <tr v-for="(value, key) in post" :key="value.id">
                        <td>{{value.userId}}</td>
                        <td>{{value.id}}</td>
                        <td>{{value.title}}</td>
                        <td>{{value.body}}</td>
                        <td>
                            <div>
                                <button @click="deleteData(value.id,key)">DELETE</button>
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
    name: 'Posts',
    data() {
        return {
            loading: false,
            post: null
        }
    },
    created: function() {
        this.loading = true
        axios
            .get('https://jsonplaceholder.typicode.com/posts')
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
                .delete('https://jsonplaceholder.typicode.com/posts/' + id, {
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



