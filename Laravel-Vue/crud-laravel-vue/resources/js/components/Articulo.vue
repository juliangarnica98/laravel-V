<template>
    <div class="container">
        <button v-on:click="openModal()" type="button" class="btn btn-primary" >Nuevo article</button>

        <div class="modal" :class="{mostrar:modal}">
            <div class="modal fade" >
                <div class="modal-dialog">
                    <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">{{titulo_modal}}</h1>
                        <button v-on:click="closeModal()" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary">Save changes</button>
                    </div>
                    </div>
                </div>
            </div>
        </div>
            

        <div class="row d-flex justify-content-center ">
        <h1 class="text-center">Gestion de articulos</h1>            
            <hr>
            <table class="table">
                <thead class="thead-dark">
                    <tr>
                    <th scope="col" class="text-center">id</th>
                    <th scope="col" class="text-center">nombre</th>
                    <th scope="col" class="text-center">descripcion</th>
                    <th scope="col" class="text-center">stock</th>
                    <th scope="col" class="text-center" colspan="2">Acción</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="articulo in articulos" v-bind:key="articulo.id" >
                        <th>{{articulo.id}}</th>
                        <td>{{articulo.name}}</td>
                        <td>{{articulo.description}}</td>
                        <td>{{articulo.stock}}</td>
                        <td>
                            <button class="btn btn-warning">Editar</button>
                        </td>
                        <td>
                            <button class="btn btn-danger" v-on:click="deleteArticle(articulo.id)">Eliminar</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        
    </div>
</template>
<script>
    export default{
        data(){
            return{
                modal:0,
                articulos:[],
                titulo_modal:'',
            }
        },
        mounted(){
            this.getArticles();
        },
        methods:{
            async getArticles(){
                fetch('http://127.0.0.1:8000/api/articulo',{
                    method:'get'
                }).then(response => response.json())
                .then(data => {
                        this.articulos = data;
                })
            },
            async deleteArticle(id){
                fetch('http://127.0.0.1:8000/api/articulo/'+id,{
                    method:'delete'
                });
                this.getArticles();
            },
            async openModal(){
                this.modal = 1;
            },
            async closeModal(){
                this.modal = 0;
            }
        }
    }
</script>
<style>
.mostrar{
    display: list-item;
    opacity: .5;
    background: rgb(28, 28, 69);
}
</style>