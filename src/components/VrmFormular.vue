<template>
  <div class="form-holder">

    <!-- Add new from -->
    <form @submit.prevent="submitForm" v-if="!formData">
      <h2>Add new Form</h2>
      <label>Title:</label>
      <input v-model="title" maxlength="100">
      <label>Text:</label>
      <textarea v-model="text" maxlength="300"></textarea>
      <label>{{ text.length }}/300 characters used</label>
      <label>Date:</label>
      <input v-model="date" type="date">
      <button type="submit">Add</button>
    </form>

    <!-- Edit from -->
    <form v-if="formData">
      <h2>Edit Form</h2>
      <label>Title:</label>
      <input v-model="editFormData.title" maxlength="100">
      <label>Text:</label>
      <textarea v-model="editFormData.text" maxlength="300"></textarea>
      <label>{{ editFormData.text.length }}/300 characters used</label>
      <label>Date:</label>
      <input v-model="editFormData.date" type="date">
      <button @click="updateForm">Save</button>
      <button @click="cancelForm">Cancel</button>
    </form>
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
export default {
  name: 'VrmFormular',
  props: {
    formData: {
      type: Object,
      default() {
        return null
      }
    }
  },
  data() {
    return {
      title: '',
      text: '',
      date: '',
      editFormData: {}
    }
  },
  watch: {
    formData(data) {
      this.editFormData = {...data}
    }
  },
  methods: {
    submitForm() {
      this.$emit('form-submitted', {
        id: nanoid(), 
        title: this.title, 
        text: this.text, 
        date: this.date
      });
      this.resetForm();
    },
    resetForm() {
      this.id = ''
      this.title = '';
      this.text = '';
      this.date = '';
    },
    updateForm() {
      this.$emit('form-updated', this.editFormData);
    },
    cancelForm() {
      this.$emit('form-cancelled');
    },
  }
}
</script>

<style scoped lang="scss">

// Variables
$primary-color: #000000;
$secondary-color: #ffffff;
$light-gray: #F3F6F9;

.form-holder {
  width: 100%;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
}

form {
  width: 100%;
  max-width: 400px;
  background-color: $secondary-color;
  padding: 30px;
  border-radius: 12px;

  h2 {
    margin-bottom: 30px;
  }

  label {
    color: $primary-color;
    display: block;
    text-align: left;
    margin-bottom: 5px;
  }

  input, textarea {
    display: inline-block;
    width: 100%;
    margin-bottom: 10px;
    padding: 12px;
    border: solid 1px $primary-color;
    border-radius: 4px;
    box-sizing: border-box;
    outline-style: none;
    background-color: $light-gray;
  }

  textarea {
    height: 200px;
    resize: vertical;
  }

  button {
    background-color: $primary-color;
    color: $secondary-color;
    width: 100%;
    padding: 14px 20px;
    border: none;
    border-radius: 4px;
    margin-top: 20px;
    font-weight: bold;
    cursor: pointer;

    &:hover {
      background-color: lighten($primary-color, 20%);
    }
  }
}

</style>
