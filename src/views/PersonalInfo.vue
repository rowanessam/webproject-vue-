<template>
    <div class="main">
        <div class="sidebar">
            <router-link to="/profile">
                <a href="#">
                    <i><font-awesome-icon :icon="['fas', 'user']" /></i>
                    My account
                </a>
            </router-link>
            <br><hr>
            <router-link to="/orders">
                <a href="">
                    <i><font-awesome-icon :icon="['fas', 'box-open']" /></i>
                    My Orders
                </a>
            </router-link>
            <br>
            <hr>
            <router-link to="/personalinfo">
                <a href="#" class="personal active">
                    <i><font-awesome-icon :icon="['fas', 'user-edit']" /></i>
                    Personal info
                </a>
            </router-link>
            <br />
            <hr  v-if="count==1"/>
            <router-link to="/addproduct" v-if="count==1">
                <a href="#" class="personal">
                    <i><font-awesome-icon :icon="['fas', 'user-edit']" /></i>
                    Add product
                </a>
            </router-link>

            <!--  <router-link to="/changepassword">
        <a @click="gotopass()">
            <i><font-awesome-icon :icon="['fas', 'lock']" /></i>
            Change Password
        </a>
    </router-link>
    <a @click="gotopass()">
        <i><font-awesome-icon :icon="['fas', 'lock']" /></i>
        Change Password
    </a>
      -->
            <br><hr>
            <router-link to="/">
                <a href="#">
                    <i><font-awesome-icon :icon="['fas', 'door-open']" /></i>
                    Sign out
                </a>
            </router-link>
        </div>
        <div class="mainsection">
            <form v-on:submit.prevent action="#" method="post" class="container">
                <h2>Personal Information</h2>
                <label v-if="count==0">
                    <h4>First Name:</h4>
                    <input type="text" v-model="input.First_Name">
                </label>

                <label v-if="count==0">
                    <h4>Last Name:</h4>
                    <input type="text" value=this.input.Last_Name v-model="input.Last_Name">
                </label>
                <label v-if="count==0">
                    <h4>Email Address:</h4>
                    <input type="text" value="sim.rowan.essam@alexu.edu.eg" v-model="input.Email">
                </label>
                <label v-if="count==0">
                    <h4>Phone Number</h4>
                    <input type="tel" value="012********" v-model="input.Phone">
                </label>
                <label v-if="count==0">
                    <h4>Age</h4>
                    <input type="number" min="0" max="100" style="width:200px" value="012********" v-model="input.Age">
                </label>
                <label v-if="count==0">
                    <h4>Address</h4>
                    <input type="text" value="012********" v-model="input.Address">
                </label>
                <label v-if="count==0">
                    <h4>Gender</h4>
                    <input type="text" value="female" v-model="input.Gender">

                </label>



                <label v-if="count==1">
                    <h4>Brand Name:</h4>
                    <input type="text" v-model="input1.Name">
                </label>
                <label v-if="count==1">
                    <h4>Brand Logo:</h4>
                    <input type="text" v-model="input1.Logo">
                </label>
                <label v-if="count==1">
                    <h4>Email Address:</h4>
                    <input type="text" value="sim.rowan.essam@alexu.edu.eg" v-model="input1.Email">
                </label>

                <label v-if="count==1">
                    <h4>Phone Number</h4>
                    <input type="tel" value="012********" v-model="input1.Phone">
                </label>
                <label v-if="count==1">
                    <h4>About Brand</h4>
                    <input type="tel" value="About" v-model="input1.About">
                </label>

                <label v-if="count==0">
                    <h4>Current Password:</h4>
                    <input type="password" value="Roro" id="myInput1" v-model="input.oldpass">
                    <label class="ic " v-on:click="myfunction1" id="app">Show</label>
                </label>
                <label v-if="count==0">
                    <h4>New Password:</h4>
                    <input type="password" value="Roro" id="myInput2" v-model="input.Password">
                    <label class="ic " v-on:click="myfunction2" id="app">Show</label>
                </label>
                <label v-if="count==0">
                    <h4>Confirm Password:</h4>
                    <input type="password" value="Roro" id="myInput3" v-model="input.confirm">
                    <label class="ic " v-on:click="myfunction3" id="app">Show</label>
                </label>
                <button v-if="count==0" @click="updateuser()">Save</button>


                <label v-if="count==1">
                    <h4>Current Password:</h4>
                    <input type="password" value="Roro" id="myInput1" v-model="input1.oldpass">
                    <label class="ic " v-on:click="myfunction1" id="app">Show</label>
                </label>
                <label v-if="count==1">
                    <h4>New Password:</h4>
                    <input type="password" value="Roro" id="myInput2" v-model="input1.Password">
                    <label class="ic " v-on:click="myfunction2" id="app">Show</label>
                </label>
                <label v-if="count==1">
                    <h4>Confirm Password:</h4>
                    <input type="password" value="Roro" id="myInput3" v-model="input1.confirm">
                    <label class="ic " v-on:click="myfunction3" id="app">Show</label>
                </label>
                <button v-if="count==1" @click="updatebrand()">Save</button>













            </form>    



        </div>




    </div>
</template>
<script>
    import axios from "axios"
    export default {

        name: "AppHeader",

        data: function () {
            return {
                users: "",
                loading: false,
                x: null,
                count:0,
                input: {
                    User_Name: "",
                    First_Name: "",
                    Last_Name: "",
                    Password:"",
                    confirm:"",
                    Age: "",
                    Email: "",
                    Phone: "",
                    Address: "",
                    Gender: "",
                    oldpass:""

                },
                input1: {
                    ID:"",
                    Name: "",
                    Email: "",
                    Logo:"",
                    Password: "",
                    Phone: "",
                    About:"",
                    confirm: "",
                    oldpass: ""
                },

            }
        },
        beforeMount() {


            this.loading = true;
            var u = localStorage.getItem('users')

            var p = localStorage.getItem('brand')
            if (u == '') {
                axios
                    .get('http://localhost/API/api/read_singleebrand.php?Name=' + p)
                    .then(response => (console.log(response.data),
                        this.x = response.data,
                        console.log(this.x)),
                        this.count = 1
                    )


                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


            }
            else {
                axios
                    .get('http://localhost/API/api/read_single.php?User_Name=' + u)
                    .then(response => (console.log(response.data),
                        this.x = response.data,
                        console.log(this.x))
                    )

                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                this.count = 0
            }


        },

        methods: {
            logout: function () {
                this.loading = true;
                localStorage.setItem('users', "")

                localStorage.setItem('brand', "")
                this.$router.push({ name: 'Home' })
            },
            goto: function () {

                this.$router.push({ name: 'personalinfo' })

            },
            gotopass: function () {
                this.$router.push({ name: 'changepass' })


            },
            updatebrand: function () {
                if (this.input1.Name == "") {
                    this.input1.Name = this.x.name
                }
                
                if (this.input1.Phone == "") {
                    this.input1.Phone = this.x.phone
                }
                if (this.input1.About == "") {
                    this.input1.About = this.x.about
                }
                if (this.input1.Logo == "") {
                    this.input1.Logo = this.x.logo
                }
                if (this.input1.Email == "") {
                    this.input1.Email = this.x.email
                }
                if (this.input1.oldpass == "") {
                    this.input1.oldpass = this.x.password
                    this.input1.Password = this.x.password

                }
                else if (this.input1.oldpass == this.x.password) {
                    if (this.input1.Password == "") {
                        this.input1.oldpass = this.x.password
                    }
                    else {
                        if (this.input1.Password != this.input1.confirm) {
                            this.input1.Password = ""
                            alert("the comfirmation Password not equal new password")
                        }
                        else {
                            alert("Updated successfully")
                        }
                    }
                }
                else if (this.input1.oldpass != this.x.password) {
                    alert("you have enterd wrong password")
                }
                else {
                    this.input1.Password == ""
                    this.input1.confirm = ""
                    alert("Cannot Update Password")
                }

                var brand = localStorage.getItem('brand')


                this.input1.Name = brand
                this.input1.ID = this.x.id;
                axios.post("http://localhost/API/api/updatebrand.php", this.input1)

                    .then((result) => { console.log(result) })

                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


            },

            updateuser: function () {
                if (this.input.First_Name == "") {
                    this.input.First_Name = this.x.firstname
                }
                if (this.input.Last_Name == "") {
                    this.input.Last_Name = this.x.lastname
                }
                if (this.input.Age == "") {
                    this.input.Age = this.x.age
                }
                if (this.input.Address == "") {
                    this.input.Address = this.x.address
                }
                if (this.input.Phone == "") {
                    this.input.Phone = this.x.phone
                }
                if (this.input.Gender == "") {
                    this.input.Gender = this.x.gender
                }
                if (this.input.Email == "") {
                    this.input.Email = this.x.email
                }
                if (this.input.oldpass == "") {
                    this.input.oldpass = this.x.password
                    this.input.Password = this.x.password

                }
                else if (this.input.oldpass == this.x.password) {
                    if (this.input.Password == "") {
                        this.input.oldpass = this.x.password
                    }
                    else{
                        if (this.input.Password != this.input.confirm) {
                            this.input.Password = ""
                            alert("the comfirmation Password not equal new password")
                        }
                        else {
                            alert("Updated successfully")
                        }
                    }
                }
                else if (this.input.oldpass != this.x.password) {
                    alert("you have enterd wrong password")
                }
                else {
                    this.input.Password == ""
                    this.input.confirm = ""
                    alert("Cannot Update Password")
                }

                var user = localStorage.getItem('users')
             

                this.input.User_Name = user
          
                axios.post("http://localhost/API/api/update.php", this.input)

                    .then((result) => { console.log(result) })

                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


            },
            myfunction1: function () {
                var x = document.getElementById("myInput1");
                if (x.type === "password") {
                    x.type = "text";
                    x.style.color = "#dc3545";
                }
                else {
                    x.type = "password";
                }
            },
            myfunction2: function () {
                var x = document.getElementById("myInput2");
                if (x.type === "password") {
                    x.type = "text";
                    x.style.color = "#dc3545";
                }
                else {
                    x.type = "password";
                }
            },
            myfunction3: function () {
                var x = document.getElementById("myInput3");
                if (x.type === "password") {
                    x.type = "text";
                    x.style.color = "#dc3545";
                }
                else {
                    x.type = "password";
                }
            }

        },


       

  
  }


</script>
<style scoped>
.main{
    display: flex;
    width: 80%;
    margin: auto;
    margin-top: 100px;
    margin-bottom: 100px;
}
.main .sidebar{
    flex-grow: 1;
    margin-right: 50px;
    border: 3px #000 solid;
    background-color: #fadcda;
    padding-top: 30px;
    padding-bottom: 30px;
    height: 350px;
}
.main .sidebar .personal{
    padding-bottom: 50px;
    margin-bottom: 20px;
}
.main .sidebar a{
    color: black;
    font-size: 20px;
    margin: 20px;
    padding-top: 30px;
}
.main .sidebar a:hover{
    text-decoration: none;
    color: #dc3545;
}
.main .sidebar .active{
    color: #dc3545;
}
.main .mainsection{
flex-grow: 4;
border: 3px #000 solid;
padding-bottom: 30px;

}
.main .mainsection .container .email{
    margin-left: 150px;
    margin-top: 10px;
}
.main .mainsection .container .mail{
    margin-left: 100px;
    margin-bottom: 50px;
}

.main .mainsection{
flex-grow: 4;
border: 3px #000 solid;
padding-bottom: 30px;
}
.main .mainsection .container{
    width: 90%;
    display: flex;
    flex-direction: column;
}
.main .mainsection h2{
    text-align: center;
    color: #dc3545;
}
.main .mainsection h4{
    color: #000;
}
.main .mainsection input{
    border: 0px;
    border-bottom: 2px solid #000;
    outline: none;
    color: #000;
   
    margin-bottom: 20px;
}
.main .mainsection input:focus{
    border-bottom: 2px solid #dc3545;
}
.main .mainsection .container label:focus-within h4{
    color: #dc3545;
}
.main .mainsection .container .mail{
    color: #043b5f;
    margin-bottom: 20px;
}
.main .mainsection .container select{
    border: 0px;
    width: 200px;
    color: #000;
    margin-bottom: 20px;
    border-bottom: 2px solid #000;
}
.main .mainsection .container select:focus{
    border: 0px;
    outline: none;
    border-bottom: 2px solid #dc3545;
}
.main .mainsection button{
    text-align: center;
    background-color: #fadcda;
    color: #000;
    width: 100%;
    height: 40px;
    font-size: 20px;
}
.main .mainsection button:hover{
    background-color: #dc3545;
}
    .main .mainsection h2 {
        text-align: center;
        color: #dc3545;
        margin-bottom: 50px;
        margin-top: 30px;
    }

    .main .mainsection h4 {
        color: #000;
    }

    .main .mainsection input {
        border: 0px;
        border-bottom: 2px solid #000;
        outline: none;
        color: #000;
        width: 300px;
        margin-bottom: 20px;
    }

        .main .mainsection input:focus {
            border-bottom: 2px solid #dc3545;
        }

    .main .mainsection .container label:focus-within h4 {
        color: #dc3545;
    }

    .main .mainsection button {
        text-align: center;
        background-color: #fadcda;
        color: #000;
        width: 100%;
        height: 40px;
        font-size: 20px;
    }

        .main .mainsection button:hover {
            background-color: #dc3545;
            color: black;
        }

    .main .mainsection .container .ic {
        margin-left: -50px;
        color: #043b5f;
    }

        .main .mainsection .container .ic:hover {
            color: #dc3545;
        }

    .main .mainsection #app {
        color: black;
    }

        .main .mainsection #app:hover {
            color: #dc3545;
        }
</style>