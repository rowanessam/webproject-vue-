<template>
    <div class="main">
        <div class="sidebar">
            <router-link to="/profile">
                <a href="#" class="active">
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
                <a href="#" class="personal">
                    <i><font-awesome-icon :icon="['fas', 'user-edit']" /></i>
                    Personal info
                </a>
            </router-link>
            <br />
            <hr v-if="count==11" />
            <router-link to="/addproduct" v-if="count==11">
                <a href="#" class="personal">
                    <i><font-awesome-icon :icon="['fas', 'user-edit']" /></i>
                    Add product
                </a>
            </router-link>
            <!--
        <router-link to="/changepassword" >
        <a href="#">
            <i><font-awesome-icon :icon="['fas', 'lock']" /></i>
            Change Password
        </a>
        </router-link>-->
            <br><hr>
            <a @click="logout();">
                <i><font-awesome-icon :icon="['fas', 'door-open']" /></i>
                Sign out
            </a>
        </div>
        <div class="mainsection" v-if="count==10">

            <h5  class="one">
                User Name:
                <span>
                    {{x.username}}
                </span>
            </h5>


            <h5  class="two">
                First Name:
                <span>
                    {{x.firstname}}
                </span>
            </h5>

            <h5  class="two">
                Last Name:
                <span>
                    {{x.lastname}}
                </span>
            </h5>
            <br />
            <h5 class="two">
                Email:
                <span>
                    {{x.email}}
                </span>
            </h5>

           

            <h5  class="two">
                Your Address
                <span>
                    {{x.address}}
                </span>
            </h5>
            <br>
            <h5 class="two">
                Age:
                <span>
                    {{x.age}}
                </span>
            </h5>
            <br />
            <h5 class="two">
                Phone:
                <span>
                    {{x.phone}}
                </span>
            </h5>
            <br />
            <button @click="goto()" class="edit">Edit</button>




        </div>

        <div class="mainsection" v-if="count==11">

           

            <h5 class="one" >
                Brand Name:
                <span>
                    {{x.name}}
                </span>
            </h5>

           
            <br />
            <h5 class="two" >
                Email:
                <span>
                    {{x.email}}
                </span>
            </h5>

            <h5 class="one">
                About Brand:
                <span>
                    {{x.about}}
                </span>
            </h5>

          
           
            <h5 class="two" >
                Phone:
                <span>
                    {{x.phone}}
                </span>
            </h5>
            <br />
            <button @click="goto()" class="edit">Edit</button>




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
             

            }
        },
       

        methods: {
            logout: function () {
                this.loading = true;
                localStorage.setItem('users',"")
                localStorage.setItem('brand', "")
                this.count = 0;
                this.$router.push({ name: 'Home' })
            },
            goto: function () {

                this.$router.push({ name: 'personalinfo' })

            },
         
           
        },
       
        beforeMount() {

            this.loading = true;
            var u = localStorage.getItem('users')

            var p = localStorage.getItem('brand')
            console.log(u)
            if (u == '') {
                axios
                    .get('http://localhost/API/api/read_singleebrand.php?Name=' + p)
                    .then(response => (console.log(response.data),
                        this.x = response.data,
                        console.log(this.x)),
                       
                    )


                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                this.count = 11;
            }
            else{

                axios
                    .get('http://localhost/API/api/read_single.php?User_Name=' + u)
                    .then(response => (console.log(response.data),
                        this.x = response.data,
                        console.log(this.x))
                    )




                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)

                this.count = 10



               
            }
            console.log(this.count)
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
text-align: left;
}
.main .mainsection a{
    color: #dc3545;
    border: 2px solid #000;
    font-size: 20px;
    width: 70px;
    margin-left: 100px;
    padding: 5px 30px 5px 10px;
}
.main .mainsection a:hover{
    text-decoration: none;
    color: #fff;
    background-color: #dc3545;
    border-radius: 59px;
}
/* .main .mainsection .edit{
  
} */
.main .mainsection .one{
    padding: 30px 0px 0px 30px;
}
.main .mainsection .two{
    padding: 5px 0px 0px 30px;
}
.main .mainsection h5{
    color: #000;
    margin-left: 20px;
    padding-bottom: 10px;
}
.main .mainsection h5 span{
    color: #dc3545;
}
.main .mainsection h4{
    color: #000;
    margin-left: 50px;
    padding-bottom: 10px;
}
.main .mainsection h4 span{
    color: #dc3545;
    margin-left: 50px;
}
.main .mainsection label{
    padding-left: 100px;
}
    .edit {
        margin-left:40px;
        text-align: center;
        background-color: #fadcda;
        color: #000;
        width: 90%;
        height: 40px;
        font-size: 20px;
    }
        .edit:hover {
            background-color: #dc3545;
        }
</style>