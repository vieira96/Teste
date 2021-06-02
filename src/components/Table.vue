<template>
  <div v-if="pessoas.length" class="table">
    <h1>Pessoas cadastradas</h1>
    <table>
      <tr>
        <th>Nome completo</th>
        <th>E-mail</th>
        <th>Telefone</th>
        <th>CPF</th>
        <th>CNPJ</th>
        <th>AÇÕES</th>
      </tr>

      <TableRow v-for="pessoa in pessoas" :key="pessoa.id" :pessoa="pessoa" @destroy="$emit('destroy', $event)" @selecionaPessoa="$emit('selecionaPessoa', $event)" />

    </table>
  </div>
</template>

<script>

import TableRow from '@/components/TableRow'

export default {
  components: {
    TableRow
  },
  props: {
    pessoas: {
      type: Array
    }
  },
  computed: {
    nomeCompleto: () => {
      return this.pess
    }
  }
}
</script>

<style scoped>
  .table {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    flex-direction: column;
  }

  table {
    border-collapse: collapse;
    width: 80%;
    margin-top: 20px;
  }

  td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }

  tr:nth-child(even) {
    background-color: #dddddd;
  }
</style>