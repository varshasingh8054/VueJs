<template>
  <div class="add">
    <div class="formlayout">
      <h2>
        <Strong>{{ msg }}</strong>
      </h2>
      <form @submit.prevent="onAdd()" method="post" class="form">
        <div class="form-feild">
          <input class="input-feild" type="text" placeholder="First Name" v-model="form.firstName" autocomplete/>
          <!-- <span class="error">{{firstName}}</span> -->
        </div>
        <div class="form-feild">
          <input class="input-feild" type="text" placeholder="Last Name" v-model="form.lastName" autocomplete/>
          <!-- <span class="error">{{lastName}}</span> -->
        </div>
        <div class="form-feild">
          <input class="input-feild" type="number" placeholder="Age" v-model="form.age" autocomplete/>
          <!-- <span class="error">{{age}}</span> -->
        </div>
        <button type="submit" class="bt btn-info">Add</button>
        &nbsp;
        <button type="button" class="bt btn-info" v-on:click="update()" >Update</button>
         <!-- <button type="button" v-on:click="onUpdate()" class="bt btn-info">Update</button> -->
      </form>
    </div>
    <form class="form" v-if="show" method="post" >
      <table style="width:100%">
        <tr>
          <th>Firstname</th>
          <th>Lastname</th>
          <th>Age</th>
        </tr>
        <tr v-for="(ele, index) in array1">
          <td>{{ele.firstName}}</td>
          <td>{{ele.lastName}}</td>
          <td>{{ele.age}}</td>
           <button  type="button" v-on:click="onUpdate(index)"  class="rounded-0" variant="success">Update</button>
          &nbsp;
        <button  type="button" v-on:click="onDelete(index)"  class="rounded-0" variant="success">Delete</button>
        </tr>
        <br>
      </table>
    </form>
  </div>
  
</template>

<script>
  export default {
    name: "Add",
    data() {
      return {
        msg: "Add",
        form: {
          firstName: "",
          lastName: "",
          age: ""
        },
        array1: [],
        indexOfArray: "",
        show: false
        
      };
    },
    methods: {
      goBack() {
        window.history.length > 1 ? this.$router.go(-1) : this.$router.push("/");
      },
      onAdd() {
        this.array1.push({firstName: this.form.firstName,
                          lastName: this.form.lastName,
                          age: this.form.age});
     
        if (this.array1.length) {
          this.show = true;
        }

        alert(this.form.firstName);
        this.form= {
          firstName: "",
          lastName: "",
          age: ""
        }
      },

      onUpdate(index)
      {
        console.log("IndexOne");
         this.indexOfArray=index;
        this.form= {
          firstName: this.array1[index].firstName,
          lastName: this.array1[index].lastName,
          age: this.array1[index].age
        }
       console.log("IndexOfArray", this.indexOfArray)

      },
      update()
      {
        // console.log(indexOfArray);
        console.log(this.form.firstName)
       this.array1[this.indexOfArray].firstName=this.form.firstName,
        this.array1[this.indexOfArray].lastName= this.form.lastName,
        this.array1[this.indexOfArray].age=this.form.age
      },
      onDelete(index)
      {
        console.log("bdfjhsfs")
        this.array1.splice(index, 1);
      }

    }
  };
</script>

<style>
  /* <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous"> */
</style>