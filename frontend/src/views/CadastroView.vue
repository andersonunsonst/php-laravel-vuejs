<template>

    <div>

        <h1>Cadastrar Usuário</h1>

        <div class="container">
            <div class="row">
                <div class="col-3"></div>
                <div class="col-6">

                    <div class="my-3">
                        <label for="nome" class="form-label">Nome:</label>
                        <input type="text" class="form-control" name="nome" id="nome" required v-model="nome">
                    </div>
                    <div class="my-3">
                        <label for="cpf" class="form-label">CPF:</label>
                        <input type="text" class="form-control" name="cpf" id="cpf" required v-model="cpf">
                    </div>
                    <div class="my-3">
                        <label for="email" class="form-label">E-mail:</label>
                        <input type="email" class="form-control" name="email" id="email" required v-model="email">
                    </div>

                    <div class="my-3">
                        <label for="logradouro" class="form-label">Logradouro:</label>
                        <input type="text" class="form-control" name="logradouro" id="logradouro" v-model="logradouro">
                    </div>
                    <div class="my-3">
                        <label for="cep" class="form-label">CEP: </label>
                        <input type="text" class="form-control" name="cep" id="cep" v-model="cep">
                    </div>
                    <div class="my-3">
                        <input type="submit" value="Adcionar" @click="addUsuario" class="btn btn-primary">
                    </div>

                </div>
                <div class="col-3"></div>
            </div>

        </div>

    </div>

</template>

<script>

import axios from 'axios'

export default {

    data() {
        return {
            iduser: "",
        }

    },
    methods: {

        addUsuario() {

            var dataUsuario = { nome: this.nome, cpf: this.cpf, email: this.email, perfil_id: this.perfil_id }

            axios.post("http://127.0.0.1:8000/api/adicionar", dataUsuario).then((response) => {
                console.log(response)
                this.iduser = response.data.id

                var dataEndereco = { logradouro: this.logradouro, cep: this.cep, id_usuario: this.iduser }

                axios.post("http://127.0.0.1:8000/api/adicionarendereco", dataEndereco).then((response) => {
                    console.log(response)
                });

            });

            setTimeout(() => {
                this.$router.push('/listar')
            }, 1000);

        },


    },

};

</script>

<style>

</style>