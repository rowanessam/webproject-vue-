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
                <a href="#" class="personal ">
                    <i><font-awesome-icon :icon="['fas', 'user-edit']" /></i>
                    Personal info
                </a>
            </router-link>
            <br />
            <hr />
            <router-link to="/addproduct" v-if="count=1">
                <a href="#" class="personal active">
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
                <h2>Add Product</h2>
                

                <label>
                    <h4>Product Name:</h4>
                    <input type="text" value=this.input.Name v-model="input.Name">
                </label>
                <label>
                    <h4>Category Name:</h4>
                    <select  v-model="input.Category_Name">
                        <option name="dresses"> dresses</option>
                        <option name="skirt" > skirt</option>

                        <option name="blouses"> blouses</option>
                        <option name="blazer" >blazer</option>
                    </select>


                    <!-- <input type="text" value="cat name" placeholder="dresses" v-model="input.Category_Name">-->
                </label>
                <label>
                    <h4>Size:</h4>
                    <input type="text" value="xlarge" v-model="input.Sizes">
                </label>
                <label>
                    <h4>Color:</h4>
                    <input type="text" value="xlarge" v-model="input.Colors">
                </label>
                <label>
                    <h4>Price:</h4>
                    <input type="number" min="1" value="price" v-model="input.Price">
                </label>
                <label>
                    <h4>Quantity:</h4>
                    <input type="number" value="100" min="1"  v-model="input.quantity">
                </label>
                <label>
                    <h4>Image:</h4>
                    <input type="text" value="url" v-model="input.Description">
                </label>
                <button @click="addproduct()">Add product</button>


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
                count: 0,
                input: {
                    Name: "",
                    Derscription: "",
                    Sizes: "",
                    Brand_ID: "",
                    Category_Name: "",
                    Price: "",
                    Category_id: "",
                    Colors: "",
                    quantity: "",
                 

                },
               

            }
        },

        beforeMount() {


            this.loading = true;




        },

        methods: {
            logout: function () {
                this.loading = true;
                localStorage.setItem('users', "")

                this.$router.push({ name: 'Home' })
            },
            goto: function () {

                this.$router.push({ name: 'personalinfo' })

            },
            addproduct: function () {
                var p = localStorage.getItem('brand')
                axios
                    .get('http://localhost/API/api/read_singlecat%20.php?Name=' + this.input.Category_Name)
                    .then(response => (this.input.Category_id = response.data.id))
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


                axios
                    .get('http://localhost/API/api/read_singleebrand.php?Name=' + p)
                    .then(response => (this.input.Brand_ID = response.data.id)
                        
                    )
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


                axios
                    .post('http://localhost/API/api/createproduct.php', this.input)
                    .then(response => (console.log(response.data))

                    )
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)



            },
            checkadd: function (response) {
                if (response != '4atateeer') {
                    alert("added succefuly")
               
                }
                else {
                    alert("failed")

                }


            }  

        },





    }


</script>
<style scoped>
    .main {
        display: flex;
        width: 80%;
        margin: auto;
        margin-top: 100px;
        margin-bottom: 100px;
    }

        .main .sidebar {
            flex-grow: 1;
            margin-right: 50px;
            border: 3px #000 solid;
            background-color: #fadcda;
            padding-top: 30px;
            padding-bottom: 30px;
            height: 350px;
        }

            .main .sidebar .personal {
                padding-bottom: 50px;
                margin-bottom: 20px;
            }

            .main .sidebar a {
                color: black;
                font-size: 20px;
                margin: 20px;
                padding-top: 30px;
            }

                .main .sidebar a:hover {
                    text-decoration: none;
                    color: #dc3545;
                }

            .main .sidebar .active {
                color: #dc3545;
            }

        .main .mainsection {
            flex-grow: 4;
            border: 3px #000 solid;
            padding-bottom: 30px;
        }

            .main .mainsection .container .email {
                margin-left: 150px;
                margin-top: 10px;
            }

            .main .mainsection .container .mail {
                margin-left: 100px;
                margin-bottom: 50px;
            }

        .main .mainsection {
            flex-grow: 4;
            border: 3px #000 solid;
            padding-bottom: 30px;
        }

            .main .mainsection .container {
                width: 90%;
                display: flex;
                flex-direction: column;
            }

            .main .mainsection h2 {
                text-align: center;
                color: #dc3545;
            }

            .main .mainsection h4 {
                color: #000;
            }

            .main .mainsection input {
                border: 0px;
                border-bottom: 2px solid #000;
                outline: none;
                color: #000;
                margin-bottom: 20px;
            }

                .main .mainsection input:focus {
                    border-bottom: 2px solid #dc3545;
                }

            .main .mainsection .container label:focus-within h4 {
                color: #dc3545;
            }

            .main .mainsection .container .mail {
                color: #043b5f;
                margin-bottom: 20px;
            }

            .main .mainsection .container select {
                border: 0px;
                width: 200px;
                color: #000;
                margin-bottom: 20px;
                border-bottom: 2px solid #000;
            }

                .main .mainsection .container select:focus {
                    border: 0px;
                    outline: none;
                    border-bottom: 2px solid #dc3545;
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