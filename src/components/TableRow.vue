<template>
  <tr>
    <td>{{nomeCompleto}}</td>
    <td>{{pessoa.email}}</td>
    <td>{{pessoa.telefone}}</td>
    <td>{{pessoa.cpf}}</td>
    <td>{{pessoa.cnpj}}</td>
    <td>
      <button @click.stop.prevent="$emit('destroy', pessoa)">Deletar</button>
      <button @click.stop.prevent="$emit('selecionaPessoa', pessoa)">Editar</button>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    pessoa: {
      typeof: Object
    }
  },
  computed: {
    nomeCompleto: function() {
      return `${this.pessoa.nome}  ${this.pessoa.sobrenome}`;
    }
  }
}
</script>