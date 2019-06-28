<template>
  <div class="add">
    <div class="formlayout">
      <div class="form-feild" v-if="updateButton"> 
      <h2>
      <Strong>{{ msg1 }}</strong>
      </h2>
      </div>
      <div class="form-feild" v-if="!updateButton"> 
      <h2>
      <Strong>{{ msg }}</strong>
      </h2>
      </div>
      <form @submit.prevent="onAdd()" method="post" class="form" >
        <div class="form-feild">
          <input class="input-feild" type="text" placeholder="First Name" v-model="form.firstName" autocomplete/>
        </div>
        <div class="form-feild">
          <input class="input-feild" type="text" placeholder="Last Name" v-model="form.lastName" autocomplete/>
        </div>
        <div class="form-feild">
          <input class="input-feild" type="number" placeholder="Age" v-model="form.age" autocomplete/>
        </div>
        <div class="form-feild" v-if="!updateButton" >
          <button type="submit" class="bt btn-info">Add</button> &nbsp;
        </div>
        <div class="form-feild" v-if="updateButton" >
          <button type="button"  v-on:click="update()" class="bt btn-info">Update</button> &nbsp;
        </div>
      </form>
    </div>

    <form class="form" v-if="show" method="post">
      <table style="width:100%">
        <tr>
          <!-- <th>Email</th> -->
          <th>Firstname</th>
          <th>Lastname</th>
          <th>Age</th>
        </tr>
        <tr v-for="(ele, index) in localSto">
          <!-- <td>{{ele.email}}</td> -->
          <td>{{ele.firstName}}</td>
          <td>{{ele.lastName}}</td>
          <td>{{ele.age}}</td>
          <button type="button" v-on:click="onUpdate(index)" class="rounded-0" variant="success">Update</button> &nbsp;
          <button type="button" v-on:click="onDelete(index)" class="rounded-0" variant="success">Delete</button>
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
          msg1: "Update",
        form: {
          // email: "",
          firstName: "",
          lastName: "",
          age: ""
        },
        array1: [],
        indexOfArray: "",
        show: true,
        updateButton: false,
        localSto: JSON.parse(localStorage.getItem("user"))
      };
    },
    methods: {
            myFunctionOnLoad(){
           this.array1 = this.array1.concat(this.localSto);
        },
      onAdd() {
        if(this.form.firstName!= '')
        {
        this.array1.push({
          // email: this.form.email,
          firstName: this.form.firstName,
          lastName: this.form.lastName,
          age: this.form.age
        });
        if (this.array1.length) {
          localStorage.setItem("user", JSON.stringify(this.array1));
           localStorage.setItem("user1", JSON.stringify(this.form));
          this.show = true;
        }
        }
        console.log("SHOW VALUE", this.array1);
        this.localSto = JSON.parse(localStorage.getItem("user"));
        console.log(this.localSto);
        // alert(this.form.firstName);
        this.form = {
          // email: " ",
          firstName: "",
          lastName: "",
          age: ""
        };
      },
  
      onUpdate(index) {
        this.updateButton= true;
        console.log("IndexOne",this.updateButton);
        this.indexOfArray = index;
        this.form = {
          //  email: this.array1[index].email,
           firstName: this.array1[index].firstName,
          lastName: this.array1[index].lastName,
          age: this.array1[index].age
        };
        //  localStorage.setItem("user", this.array1);
        console.log("IndexOfArray", this.indexOfArray);
      },
  
      update() {
        // console.log(indexOfArray);
        // console.log(this.form.firstName);
        //  this.array1 = this.array1.concat(this.localSto);
        // (this.array1[this.indexOfArray].email = this.form.email),
        (this.array1[this.indexOfArray].firstName = this.form.firstName),
        (this.array1[this.indexOfArray].lastName = this.form.lastName),
        (this.array1[this.indexOfArray].age = this.form.age);
       
        localStorage.setItem("user", JSON.stringify(this.array1));
        this.localSto = JSON.parse(localStorage.getItem("user"));
        console.log(this.localSto.length);
        //  this.updateButton= false;
      },
  
      onDelete(index) {
        console.log("Index",index)
        localStorage.setItem("user", JSON.stringify(this.array1));
        this.localSto = JSON.parse(localStorage.getItem("user"));
         console.log("sdfjsdfhsdhj",this.localSto);
      }
    },
      created: function(){
        this.myFunctionOnLoad()
      }
  }
</script>

<style>
  /* <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous"> */
</style>