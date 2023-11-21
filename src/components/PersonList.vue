<template>
  <div>
    <ul>
      <li v-for="person in people" :key="person.id">
        Nome: {{ person.name }} <br><br>
        Data de Nascimento: {{ person.birthdate }} <br><br>
        CPF: {{ person.cpf }}<br><br>
        
        <button @click="editPerson(person)">Editar</button>
        <button @click="deletePerson(person.id)">Excluir</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['people'],
  methods: {
    editPerson(person) {
      this.$emit('edit', person);
    },
    deletePerson(personId) {
      this.$emit('delete', personId);
    }
  }
};
</script>
