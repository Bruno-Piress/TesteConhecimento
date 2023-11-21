<template>
  <div>
    <person-form
    :personToEdit="personToEdit"
    @submit="submitForm"
    ></person-form>
    <person-list
      :people="people"
      @edit="editPerson"
      @delete="deletePerson"
    ></person-list>
  </div>
</template>

<script>
import PersonList from './components/PersonList.vue';
import PersonForm from './components/PersonForm.vue';
import './assets/style.css'

export default {
  data() {
    return {
      people: [],
      personToEdit: null
    };
  },
  methods: {
    editPerson(person) {
      this.personToEdit = person;
    },
    deletePerson(personId) {
      this.people = this.people.filter(person => person.id !== personId);
    },
    submitForm(formData) {
      if (this.personToEdit) {
        const index = this.people.findIndex(person => person.id === this.personToEdit.id);
        this.people[index] = { ...formData, id: this.personToEdit.id };
        this.personToEdit = null;
      } else {
        this.people.push({ ...formData, id: Date.now() });
      }
    }
  },
  components: {
    PersonList,
    PersonForm
  }
};
</script>
