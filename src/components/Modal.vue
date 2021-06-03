<template>
  <div class="modal flex column">
    <h2>Atualizar pessoa</h2>
    <form class="flex column" @submit.stop.prevent="update(pessoa)">
      <input v-model="pessoa.nome" type="text" name="" placeholder="Informe o nome">
      <input v-model="pessoa.sobrenome" type="text" name="" placeholder="Informe o sobrenome">
      <input v-model="pessoa.email" type="email" name="" placeholder="Informe o email">
      <input v-model="pessoa.telefone" type="text" name="" placeholder="Informe o telefone">
      <div>
        <input type="checkbox" name="juridica" value="juridica" v-model="juridica">
        <label style="color: white; margin-left: 5px;" for="juridica">Pessoa juridica</label>
      </div>

      <input v-if="showCnpj" v-model="pessoa.cnpj" type="text" placeholder="Informe cnpj">
      <input v-if="showCpf" v-model="pessoa.cpf" type="text" placeholder="Informe o cpf">

      <button>Salvar</button>
      <button @click.stop.prevent="$emit('cancel')">Cancelar</button>

    </form>
  </div>
</template>

<script>
export default {
  props: {
    pessoaSelecionada: {
      type: Object,
    }
  },
  data() {
    return {
      pessoa: {},
      juridica: false,
      showCpf: true,
      showCnpj: false,
    }
  },
  watch: {
    juridica: function(val) {
      if(val === true) {
        this.showCnpj = true;
        this.showCpf = false;
        this.pessoa.cpf = '';
      } else {
        this.showCnpj = false;
        this.showCpf = true;
        this.pessoa.cnpj = '';
      }

    }
  },

  methods: {
    update(pessoa) {
      //atualizo o dado pra saber se o usuario alterou pra pessoa fisica ou juridica.
      pessoa.juridica = this.juridica
      console.log(pessoa);
      this.$emit('update', pessoa)
    }
  },
  created() {
    //Clono o objeto para nao dar problema caso eu cancele.
    this.pessoa = Object.assign({}, this.pessoaSelecionada);
    //verifico se tem um cnpj, se sim, coloco juridica como verdadeiro para o checkbox abrir ativado.
    this.pessoaSelecionada.cnpj ? this.juridica = true : this.juridica = false;
  }
}
</script>

<style scoped>
  .modal {
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    justify-content: center;
    align-items: center;
    background-color: rgba(0, 0, 0, 0.9);
  }

  .flex {
    display: flex;
  }
  .column {
    flex-direction: column;
  }

  form {
    margin-top: 10px;
    width: 300px;
  }

  form input {
    padding: 8px;
    margin-bottom: 4px;
  }
  

  button {
    padding: 5px;
    cursor: pointer;
    margin-bottom: 2px;
  }
</style>