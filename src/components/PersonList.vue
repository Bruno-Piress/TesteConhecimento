<template>
  <div>
    <h2 class="flex justify-center text-bold text-2xl mb-4 mt-4">CADASTROS:</h2>

    <div class="flex justify-center">
      <ul class="flex">
        <li
          class="mb-4 mr-6 rounded-md bg-slate-200"
          v-for="person in people"
          :key="person.id"
        >
          <div><strong>Nome:</strong> {{ person.name }}</div>
          <div><strong>Data de Nascimento:</strong> {{ person.birthdate }}</div>
          <div><strong>CPF:</strong> {{ person.cpf }}</div>
          <div><strong>CEP:</strong> {{ person.cep }}</div>
          <div><strong>Rua:</strong> {{ person.logradouro }}</div>
          <div><strong>Bairro:</strong> {{ person.bairro }}</div>
          <div><strong>Município:</strong> {{ person.localidade }}</div>
          <div><strong>Estado:</strong> {{ person.uf }}</div>


          <div class="flex justify-center mt-4 mb-4">
            <q-btn
              class="mr-2"
              color="primary"
              icon="edit"
              @click="editPerson(person)"
              >Alterar</q-btn
            >
            <q-btn
              color="negative"
              icon="delete"
              @click="confirmDelete(person.id)"
              >Excluir</q-btn
            >
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ["people"],
  methods: {
    editPerson(person) {
      this.$emit("edit", person);
    },
    confirmDelete(personId) {
      if (window.confirm("Tem certeza que deseja excluir esta pessoa?")) {
        this.$emit("delete", personId);
      }
    },
  },
};
</script>
