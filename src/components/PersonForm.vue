<template>
  <div class="flex justify-center">
    <form @submit.prevent="submitForm">
      <h2 class="text-bold flex justify-center text-4xl mt-4	">CADASTRO:</h2>

      <h4 class="text-bold flex justify-center">Dados Pessoais:</h4>

      <div class="flex justify-center">
        <q-input
          outlined
          class="w-64 mr-2 mb-2"
          label="Nome Completo:"
          v-model="formData.name"
          required
        />

        <q-input
          outlined
          class="w-64 mr-2 mb-2"
          label="Data de Nascimento:"
          type="date"
          v-model="formData.birthdate"
          required
        />

        <q-input
          outlined
          mask="###.###.###-##"
          class="w-64 mr-2 mb-2"
          label="CPF:"
          v-model="formData.cpf"
          required
        />
      </div>

      <h4 class="text-bold flex justify-center">Endereço:</h4>

      <div class="flex justify-center">
        <q-input
          outlined
          class="w-50 mr-2 mb-2"
          label="CEP:"
          mask="#####-###"
          v-model="formData.cep"
          id="cep"
          name="cep"
          @blur="buscarCep"
        />

        <q-input
          label="Rua:"
          class="mr-2 mb-2"
          outlined
          v-model="formData.logradouro"
          id="logradouro"
          name="logradouro"
        />

        <q-input
          outlined
          label="Bairro:"
          class="mr-2 mb-2"
          v-model="formData.bairro"
          id="bairro"
          name="bairro"
        />

        <q-input
          outlined
          label="Município:"
          class="mr-2 mb-2"
          v-model="formData.localidade"
          id="localidade"
          name="localidade"
        />

        <q-input
          outlined
          label="Estado:"
          class="mr-2 mb-2"
          v-model="formData.uf"
          id="uf"
          name="uf"
        />
      </div>

      <h4 class="text-bold flex justify-center ">Contatos:</h4>

      <div class="flex justify-center">
        <q-input
          outlined
          mask="(##)# ####-####"
          class="w-50 mr-2 mb-2"
          label="Celular:"
          v-model="formData.celular"
          id="celular"
          name="celular"
        />

        <q-input
          outlined
          mask="####-####"
          class="w-50 mr-2 mb-2"
          label="Telefone Residencial:"
          v-model="formData.telresidencial"
          id="telresidencial"
          name="telresidencial"
        />

        <q-input
          outlined
          mask="####-####"
          class="w-50 mr-2 mb-2"
          label="Telefone Comercial:"
          v-model="formData.telcomercial"
          id="telcomercial"
          name="telcomercial"
        />

        <q-input
          outlined
          class="w-50 mr-2 mb-2"
          label="E-mail:"
          v-model="formData.email"
          id="email"
          name="email"
        />
      </div>
      <br>
      <div  class="flex justify-center" >
        <q-btn type="submit" color="primary"
          >Salvar</q-btn
        >
      </div>
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
        cep: "",
        logradouro: "",
        bairro: "",
        localidade: "",
        uf: "",
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
      try {
        const response = await fetch(
          `https://viacep.com.br/ws/${this.formData.cep}/json/`
        );
        const data = await response.json();

        this.formData.cep = data.cep;
        this.formData.logradouro = data.logradouro;
        this.formData.bairro = data.bairro;
        this.formData.localidade = data.localidade;
        this.formData.uf = data.uf;
      } catch (error) {
        console.log("error");
      }
    },
  },
};
</script>
