<template>
    <div>
        <h1>Posts</h1>
        <div class="row">
            <div class="class-md-10"></div>
            <div class="class-md-2">
                <router-link :to="{name: 'create'}" class="btn btn-primary">Novo</router-link>
            </div>
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Item Name</th>
                        <th>Item Price</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="post in posts" :key="post.id">
                        <td>{{ post.id }}</td>
                        <td>{{ post.title }}</td>
                        <td>{{ post.body }}</td>
                        <td><router-link :to="{name: 'edit', params: { id: post.id }}" class="btn btn-primary">Edit</router-link></td>
                        <td><button class="btn btn-danger">Delete</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                posts: []
            }
        },

        created() {
            let uri = 'http://vuelaravelcrud.test/api/posts';
            this.axios.get(uri).then((response) => {
                this.posts = response.data.data;
            });
        }
    }
</script>