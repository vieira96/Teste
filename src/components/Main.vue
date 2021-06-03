<template>
  <div class="main">
    <h2>Cadastro de pessoas</h2>
    <form class="flex column" @submit.stop.prevent="submit()">
      <input v-model="nome" type="text" name="" placeholder="Informe o nome">
      <input v-model="sobrenome" type="text" name="" placeholder="Informe o sobrenome">
      <input v-model="email" type="email" name="" placeholder="Informe o email">
      <input v-model="telefone" type="text" name="" placeholder="Informe o telefone">
      <div>
        <input type="checkbox" name="juridica" value="juridica" v-model="juridica">
        <label for="juridica"> Pessoa juridica</label>
      </div>

      <div v-if="showCnpj">
        <input v-model="cnpj" type="text" placeholder="Informe cnpj">
      </div>
      <div v-if="showCpf">
        <input v-model="cpf" type="text" placeholder="Informe o cpf">
      </div>

      <button>Enviar</button>

    </form>

    <Table :pessoas="pessoas" @destroy="destroy($event)" @selecionaPessoa="selecionaPessoa($event)" />
    <Modal v-if="pessoaSelecionada.id" :pessoaSelecionada="pessoaSelecionada" @cancel="cancel()" @update="update($event)" />
  </div>
</template>

<script>

import Table from '@/components/Table';
import Modal from '@/components/Modal';

export default {
  name: 'Main',
  components: {
    Table,
    Modal
  },
  data() {
    return {
      nome: '',
      sobrenome: '',
      email: '',
      telefone: '',
      juridica: false,
      cpf: '',
      cnpj: '',
      showCpf: true,
      showCnpj: false,
      pessoas: [],
      pessoaSelecionada: {},
    }
  },
  watch: {
    juridica: function(val) {
      if(val === true) {
        this.showCnpj = true;
        this.showCpf = false;
        this.cpf = '';
      } else {
        this.showCnpj = false;
        this.showCpf = true;
        this.cnpj = '';
      }

    }
  },
  methods: {
    submit() {

      let pessoa = {
        nome: this.nome,
        sobrenome: this.sobrenome,
        email: this.email,
        telefone: this.telefone,
        juridica: this.juridica,
        cpf: this.cpf,
        cnpj: this.cnpj,
        id: this.pessoas.length+1
      }
      this.pessoas.unshift(pessoa);

      this.resetForm();
    },

    selecionaPessoa(pessoa) {
      this.pessoaSelecionada = pessoa;
    },

    destroy(pessoa) {
      console.log('delete', pessoa);
      let index = this.pessoas.findIndex(p => p.id === pessoa.id);
      this.pessoas.splice(index, 1);
    },

    cancel() {
      this.pessoaSelecionada = {}
    },

    update(pessoa) {
      let index = this.pessoas.findIndex(p => p.id === pessoa.id);
      this.pessoas.splice(index, 1, pessoa);
      this.pessoaSelecionada = {}
    },

    resetForm() {
      this.nome = ''
      this.sobrenome = ''
      this.email = ''
      this.telefone = ''
      this.juridica = false
      this.cpf = ''
      this.cnpj = ''
    }
  }
}
</script>

<style scoped>
  .flex {
    display: flex;
  }
  .column {
    flex-direction: column;
  }
  .main {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  form {
    margin-top: 10px;
  }

  form input {
    padding: 8px;
    margin-bottom: 4px;
  }

  button {
    padding: 5px;
    cursor: pointer;
  }
</style>
