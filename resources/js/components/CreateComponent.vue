<template>
    <div class="container">
        <h1>Criar Posts</h1>
        <form @submit.prevent="addPost">
            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Título</label>
                        <input type="text" class="form-control" v-model="post.title">
                    </div>
                </div> 
            </div>
            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Conteúdo</label>
                        <textarea class="form-control" v-model="post.body" rows="10"></textarea>
                    </div>
                </div>
            </div>
            <div>
                <button class="btn btn-success">Enviar</button>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                post:{}
            }
        },

        methods: {
            addPost(){
                let url = 'http://192.168.2.89/crud/public/api/post/create';
                this.axios.post(url, this.post).then((response) => {
                    this.$router.push({ name: 'posts' })
                });
            }
        }
    }
</script>