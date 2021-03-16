<template>
    <div class="main">
        <div class="loginbrand">


            <form id="contact" v-on:submit.prevent action="#" method="post">
                <h3 style="" class="create"> <b> Login to your Brand</b></h3>

                <!---<div class="upload-button upload-label"><b> Upload Your Brand Logo</b></div><br>
        <img class="profile-pic" src="../assets/fashion-logo.jpg" />
        <input class="file-upload" type="file" accept="image/*" />
           -->
               
                <fieldset>
                    <input name="name" placeholder="Your Brand name" type="text" v-model="input1.Name" required>
                </fieldset>
               
                <fieldset>
                    <input name="password" placeholder=" Password" type="tel" v-model="input1.Password" required>
                </fieldset>
               
                <button class="btn" @click="loginbrand();">Login</button>

            </form>



        </div>
        <div class="container">
            <form id="contact" v-on:submit.prevent action="#" method="post">
                <h3 style="" class="create"> <b> Create your Brand</b></h3>

                <!---<div class="upload-button upload-label"><b> Upload Your Brand Logo</b></div><br>
    <img class="profile-pic" src="../assets/fashion-logo.jpg" />
    <input class="file-upload" type="file" accept="image/*" />
       -->
                <fieldset>
                    <input name="logo" placeholder="Your Brand logo url" type="text"  v-model="input.Logo" required >
                </fieldset>
                <fieldset>
                    <input name="name" placeholder="Your Brand name" type="text" v-model="input.Name" required>
                </fieldset>
                <fieldset>
                    <input name="email" placeholder="Email Address" type="email" v-model="input.Email" required>
                </fieldset>
                <fieldset>
                    <input name="password" placeholder=" Password" type="tel" v-model="input.Password" required>
                </fieldset>
                <fieldset>
                    <input name="phone" placeholder=" Phone Number" type="tel" v-model="input.Phone" required>
                </fieldset>
                <fieldset>
                    <textarea name="about" placeholder="About your Brand" v-model="input.About" required></textarea>
                </fieldset>
              
                        <button class="btn" @click="addbrand();"  >Submit</button>
                  
            </form>


        </div>

    </div>
</template>
<script>
    import $ from 'jquery';
    $("#slider > div:gt(0)").hide();
    setInterval(function () {
        $('#slider > div:first')
            .fadeOut(1000)
            .next()
            .fadeIn(1000)
            .end()
            .appendTo('#slider');
    }, 3000);
</script>
<script>
    import axios from "axios";
    export default {
        name: 'brand',
        data () {
            return {
                loading: false,
               all_users:null,

                input: {
                    Name: "",
                    Logo: "",
                    Email: "",
                    Password: "",
                    Phone: "",
                    About:""

                },
                input1: {
                    Name: "",  
                    Password: "",
                  
                },

            }
    
            },


        methods: {
            addbrand: function () {

                console.log(this.input.Name)


                axios
                    .get('http://localhost/API/api/read_singleebrand.php?Name=' + this.input.Name)
                    .then(response => (this.check(response.data.name)))
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
            },
            loginbrand: function () {

                this.loading = true;

                axios
                    .get('http://localhost/API/api/read_singleebrand.php?Name=' + this.input1.Name)
                    .then(response => ( this.brand(response.data))
                 

                    )
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
             
              


            },
            brand: function (response) {
                if (response != "undefined") {
                    if (response.password == this.input1.Password) {
                        alert("login successful")
                        localStorage.setItem('brand', this.input1.Name);

                        this.$router.push({ name: 'Home' })
                    }
                    else {
                        alert("invalid password")

                        this.$router.push({ name: 'brands' })
                    }
                }
                else {
                    alert("not Found User name")

                    this.$router.push({ name: 'brands' })

                }

            },



            check: function (response) {
                console.log(response)
                if (response == undefined) {


                   axios
                      .post('http://localhost/API/api/createbrand.php', this.input)
                        .then(response => (console.log(response.data)))
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)
                    localStorage.setItem('brand', this.input.Name);
                    localStorage.setItem('users', "");
                    window.location.reload();
                    this.$router.push({ name: 'brandprofile' })

                }
                else {
                    alert('This Name is already used')

                }

            }
        },
      

        }




    
</script>

<style lang="scss" scoped>
    @import url(https://fonts.googleapis.com/css?family=Open+Sans:400italic,400,300,600);
    .btn {
        margin: auto;
        border: none;
        outline: 0;
        padding: 12px;
        color: white;
        border-radius: 25px;
        background-color: #e34135;
        text-align: center;
        cursor: pointer;
        width: 50%;
        font-size: 18px;
        margin-top: 25px;
    }

        .btn:hover {
            opacity: 0.7;
            color: black;
        }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-font-smoothing: antialiased;
        -moz-font-smoothing: antialiased;
        -o-font-smoothing: antialiased;
        font-smoothing: antialiased;
        text-rendering: optimizeLegibility;
    }

    .upload-button {
        padding: 4px;
        display: block;
        float: left;
        margin-bottom: 20px;
    }

    .profile-pic {
        max-width: 300px;
        max-height: 200px;
        display: block;
    }

    .container {
        max-width: 400px;
        width: 100%;
        margin: 0 auto;
        position: relative;
    }

    .main{
        display:flex;


    }
    .loginbrand{
        margin-left:250px;
       

    }
        .loginbrand form {

            margin-top: 500px;
            height: 600px;
        }
        .loginbrand form h3 {
            padding-top: 50px;
        
        }
    #contact input[type="text"], #contact input[type="email"], #contact input[type="tel"], #contact input[type="url"], #contact textarea, #contact button[type="submit"] {
        font: 400 12px/16px "Open Sans", Helvetica, Arial, sans-serif;
    }

    #contact {
        background: #fadcda;
        padding: 25px;
        margin: 50px 0;
    }

        #contact h1 {
            color: -webkit-linear-gradient(#fadcda, #dc3545);
            display: block;
            font-size: 30px;
            font-weight: 400;
        }

    .create {
        color: black;
        text-transform: uppercase;
        margin-bottom: 50px;
    }

    #contact h4 {
        margin: 5px 0 15px;
        display: block;
        font-size: 13px;
    }

    fieldset {
        border: medium none !important;
        margin: 0 0 10px;
        min-width: 100%;
        padding: 0;
        width: 100%;
    }

    #contact input[type="text"], #contact input[type="email"], #contact input[type="tel"], #contact input[type="url"], #contact textarea {
        width: 100%;
        border: 1px solid #CCC;
        background: #FFF;
        margin: 0 0 5px;
        padding: 10px;
    }

        #contact input[type="text"]:hover, #contact input[type="email"]:hover, #contact input[type="tel"]:hover, #contact input[type="url"]:hover, #contact textarea:hover {
            -webkit-transition: border-color 0.3s ease-in-out;
            -moz-transition: border-color 0.3s ease-in-out;
            transition: border-color 0.3s ease-in-out;
            border: 1px solid #AAA;
        }

    #contact textarea {
        height: 100px;
        max-width: 100%;
        resize: none;
    }

    #contact button[type="submit"] {
        cursor: pointer;
        width: 100%;
        border: none;
        background: #dc3545;
        color: #fadcda;
        margin: 0 0 5px;
        padding: 10px;
        font-size: 20px;
    }

        #contact button[type="submit"]:hover {
            background: -webkit-linear-gradient(#fadcda, #dc3545);
            -webkit-transition: background 0.3s ease-in-out;
            -moz-transition: background 0.3s ease-in-out;
            transition: background-color 0.3s ease-in-out;
        }

        #contact button[type="submit"]:active {
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.5);
        }

    #contact input:focus, #contact textarea:focus {
        outline: 0;
        border: 1px solid #999;
    }

    ::-webkit-input-placeholder {
        color: #888;
    }

    :-moz-placeholder {
        color: #888;
    }

    ::-moz-placeholder {
        color: #888;
    }

    :-ms-input-placeholder {
        color: #888;
    }
</style>