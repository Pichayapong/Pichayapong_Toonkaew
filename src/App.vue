<template>
    <div id="app">
        <header>
            <nav>
                <div class="logo"> <a href="">JSONPlaceholder</a></div>
                <ul class="menu">
                    <li>
                        <router-link to="posts">Posts</router-link>
                    </li>
                    <li>
                        <router-link to="comments">Comments</router-link>
                    </li>
                    <li>
                        <router-link to="albums">Albums</router-link>
                    </li>
                    <li>
                        <router-link to="photos">Photos</router-link>
                    </li>
                    <li>
                        <router-link to="todos">Todos</router-link>
                    </li>
                    <li>
                        <router-link to="users">Users</router-link>
                    </li>
                </ul>
            </nav>
        </header>
        <section class="main_container">
            <router-view />
        </section>
    </div>
</template>

<script>
require('@/assets/styles/App.css')
export default {
    name: 'App'
}
</script>
