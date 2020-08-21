<template>
    <div>
      <h1>Create Category</h1>
    <div class="container">
        
        <b-col sm="12">
            <b-form-input v-model="categoryName" placeholder=" Category Name"></b-form-input>
        </b-col><br>
        
        
        <b-button variant="info" @click="addCategory()">Add Category</b-button>
        
    </div><br>

  <br>
    <h1>Create Companies</h1>
    <div class="container">
        <b-col sm="12">
            <b-form-select v-model="selected" :options="options"></b-form-select>
        </b-col><br>
        <b-col sm="12">
            <b-form-input v-model="name" placeholder="Name"></b-form-input>
        </b-col><br>
        <b-col sm="12">
            <b-form-input v-model="contact" placeholder="Contact Number"></b-form-input>
        </b-col><br>
        
        <b-col sm="12">
            <b-form-input v-model="location" placeholder="Location"></b-form-input>
        </b-col><br>        

        
        
        <b-col sm="12">
            <b-form-textarea
            id="textarea"
            v-model="summary"
            placeholder="Company Summary..."
            rows="3"
            max-rows="6"
        >
        </b-form-textarea><br>
        <b-button variant="info" @click="addCompany()">Submit</b-button>
        </b-col>
    </div>

    
        
    </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      selected: null,
      options: [
        { value: null, text: "Select a Category" },
        { value: "5f3eab787b18e225b4c769fb", text: "Building Material" },
        {
          value: "5f3eaba97b18e225b4c769fc",
          text: "Photography and Videography",
        },
        { value: "5f3eabe07b18e225b4c769fd", text: "Wedding Venues" },
      ],

      categoryName: "",
      name: "",
      contact: "",
      location: "",
      summary: "",
      image: "",
    };
  },
  methods: {
    addCategory() {
      axios
        .post("https://znupit.herokuapp.com/category", {
          name: this.categoryName,
        })
        .then(response => {
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },

    addCompany() {
      axios
        .post("https://znupit.herokuapp.com/companies", {
          name: this.name,
          contact: this.contact,
          summary: this.summary,

          photos: [
            {
              image: this.image,
            },
          ],

          categories: [this.selected],
        })
        .then(response => {
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
</style>

