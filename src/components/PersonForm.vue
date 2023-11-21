<template>
  <div>
    <h4 class="text-bold">Cadastro:</h4>

    <form @submit.prevent="submitForm">
      <label for="name">Nome Completo: </label>
      <input v-model="formData.name" required />

      <label for="birthdate">Data de Nascimento:</label>
      <q-input outlined type="date" v-model="formData.birthdate" required />

      <label  for="cpf">CPF:</label>
      <input placeholder="###.###.###-##" v-model="formData.cpf" required />


      <h4 class="text-bold">Cadastrar Endereço:</h4>

      <div>
        <label for="cep">CEP:</label>
        <input v-model="addres.cep" id="cep" name="cep" @blur="buscarCep" />
      </div>
      <br>
      <div>
        <label for="logradouro">Rua:</label>
        <input v-model="addres.logradouro" id="logradouro" name="logradouro" />
      </div>

      <div>
        <label for="bairro">Bairro:</label>
        <input v-model="addres.bairro" id="bairro" name="bairro" />
      </div>

      <div>
        <label for="localidade">Município:</label>
        <input v-model="addres.localidade" id="localidade" name="localidade" />
      </div>

      <div>
        <label for="uf">Estado:</label>
        <input v-model="addres.uf" id="uf" name="uf" />
      </div>

      <button type="submit">Salvar</button>


    </form>
  </div>
</template>

<script>
export default {
  props: ["personToEdit"],
  data() {
    return {
      formData: {
        name: "",
        birthdate: "",
        cpf: "",
      },
      addres: {
        cep: "",
        endereco: "",
      },
    };
  },
  watch: {
    personToEdit(newVal) {
      if (newVal) {
        this.formData = { ...newVal };
      }
    },
  },
  methods: {
    submitForm() {
      this.$emit("submit", { ...this.formData });
      this.clearForm();
    },

    async buscarCep() {
        try{
          const response = await fetch(`https://viacep.com.br/ws/${this.addres.cep}/json/`)
          const data = await response.json()

          this.addres.logradouro = data.logradouro
          this.addres.bairro = data.bairro
          this.addres.localidade = data.localidade
          this.addres.uf = data.uf

        }catch(error){
          console.log('error');
        }
    },


  },
};
</script>
