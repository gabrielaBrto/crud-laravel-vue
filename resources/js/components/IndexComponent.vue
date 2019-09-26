<template>
    <div class="container">
        <h1>Posts</h1>
        <div class="row">
            <div class="class-md-10"></div>
            <div class="class-md-2 mb-4">
                <router-link :to="{name: 'create'}" class="btn btn-primary">Novo</router-link>
            </div>
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Titulo</th>
                        <th>Conteudo</th>
                        <th>Editar</th>
                        <th>Deletar</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="post in posts" :key="post.id">
                        <td>{{ post.id }}</td>
                        <td>{{ post.title }}</td>
                        <td>{{ post.body }}</td>
                         <td><router-link :to="{name: 'edit', params: { id: post.id }}" class="btn btn-warning">Editar</router-link></td>
                        <td><button class="btn btn-danger" @click.prevent="deletePost(post.id)">Deletar</button></td>
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
      let uri = 'http://localhost:8000/api/posts';
      this.axios.get(uri).then(response => {
        this.posts = response.data.data;
      });
    },
    methods: {
      deletePost(id)
      {
        let uri = `http://localhost:8000/api/post/delete/${id}`;
        this.axios.delete(uri).then(response => {
            
          this.posts.splice(this.posts.indexOf(id), 1);
        });
      }
    }

    }
</script>