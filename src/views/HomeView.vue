<template>
  <div class="container">
    <VrmFormular 
      :formData="selectedFormData" 
      @form-submitted="handleFormData" 
      @form-updated="updateFormData" 
      @form-cancelled="clearSelection"
    />
    <ul v-if="formData.length">
      <h3>Your forms:</h3>
      <li v-for="(form) in formData" :key="form.id">
        {{ form.title }} - {{ form.date }}
        <button @click="editForm(form)">Edit</button>
      </li>
    </ul>
  </div>
</template>

<script>
import VrmFormular from '@/components/VrmFormular.vue'

export default {
  data() {
    return {
      formData: [],
      selectedFormData: null,
    }
  },
  components: {
    VrmFormular
  },
  methods: {
    handleFormData(data) {
      this.formData.push(data)
    },
    editForm(form) {
      this.selectedFormData = form;
    },
    updateFormData(updatedFormData) {
      const index = this.formData.findIndex(form => form.id === updatedFormData.id);
      this.$set(this.formData, index, updatedFormData);
      this.clearSelection();
    },
    clearSelection() {
      this.selectedFormData = null;
    }
  }
}
</script>
<style scoped lang="scss">

// Variables
$primary-color: #000000;
$secondary-color: #ffffff;

// Classes
.container {
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 40px 10px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 40px 0;
  width: 100%;
  max-width: 400px;

  h3 {
    text-align: left;
    margin-bottom: 10px;
  }
}

li {
  padding: 20px;
  margin-bottom: 20px;
  background-color: $secondary-color;
  border-radius: 12px;
  text-align: left;
  display: flex;
  justify-content: space-between;
  align-items: center;
  word-break: break-all;

  &:last-child {
    margin-bottom: 0;
  }

  a {
    text-decoration: none;
    color: #333;

    &:hover {
      color: #000;
    }
  }
}

button {
  background-color: $primary-color;
  color: $secondary-color;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  margin-left: 10px;
  word-break: normal;
  cursor: pointer;
  display: block;

  &:hover {
    background-color: lighten($primary-color, 20%);
  }
}

</style>
