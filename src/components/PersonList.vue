<template>
  <div class="flex justify-center">
    <ul>
      <li
        class="flex justify-center"
        v-for="person in people"
        :key="person.id"
        style="display: block; margin-bottom: 20px"
      >
        <div>Nome: {{ person.name }}</div>

        <div>Data de Nascimento: {{ person.birthdate }}</div>

        <div>CPF: {{ person.cpf }}</div>

        <div>Rua: {{ person.logradouro }}</div>

        <div>Bairro: {{ person.bairro }}</div>

        <div>Município: {{ person.localidade }}</div>

        <div>Estado: {{ person.uf }}</div>

        <div>Celular: {{ person.celular }}</div>

        <div>Telefone Residencial: {{ person.telresidencial }}</div>

        <div>Telefone Comercial: {{ person.telcomercial }}</div>

        <div>E-mail: {{ person.email }}</div>

        <q-btn class="mr-2" color="positive" @click="editPerson(person)"
          >Editar</q-btn
        >
        <q-btn color="negative" @click="deletePerson(person.id)">Excluir</q-btn>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["people"],
  methods: {
    editPerson(person) {
      this.$emit("edit", person);
    },
    deletePerson(personId) {
      this.$emit("delete", personId);
    },
  },
};

</script>
