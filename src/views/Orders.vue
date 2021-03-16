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
                <a href="" class="active">
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
            <br>
            <hr v-if="count==1">
            <router-link to="/addproduct" v-if="count==1">
                <a href="#" class="personal ">
                    <i><font-awesome-icon :icon="['fas', 'user-edit']" /></i>
                    Add product
                </a>
            </router-link>
            <!-- <br>
        <router-link to="/changepassword" >
        <a href="#">
            <i><font-awesome-icon :icon="['fas', 'lock']" /></i>
            Change Password
        </a>
        </router-link>-->
            <br><hr>
            <router-link to="/">
                <a href="#">
                    <i><font-awesome-icon :icon="['fas', 'door-open']" /></i>
                    Sign out
                </a>
            </router-link>
        </div>
        <div v-if="count==0" class="mainsection">

            <table style="width:40%; margin-right:1px; margin-left:1px">
                <tr>
                    <th>Order number</th>

                </tr>
                <tr v-for="order in orders" v-bind:key="order">
                    <td>{{order.id}}</td>

                </tr>
            </table>


            <table style="width:40%; margin-right:1px">
                <tr>

                    <th>Product name</th>

                </tr>
                <tr v-for="nam in name" v-bind:key="nam">

                    <td>{{nam}}</td>
                </tr>
            </table>

            <table>
                <tr>


                    <th>Quantity</th>
                    <th>Total price</th>
                    <th>Order Date</th>
                    <th>Delivery Date</th>
                </tr>
                <tr v-for="order in orders" v-bind:key="order">

                    <td>{{order.quantity}}</td>
                    <td>{{order.total_price}}</td>
                    <td>{{order.order_date}}</td>
                    <td>{{order.delivery_data}}</td>
                </tr>
            </table>

        </div>


        <div v-else class="mainsection">

            <table style="width:60%; margin-right:1px; margin-left:1px">
                <tr>
                    <th>Order number</th>
                    <th>User Name</th>
                </tr>
                <tr v-for="order in product" v-bind:key="order">
                    <td>{{order.id}}</td>
                    <td>{{order.username}}</td>

                </tr>
            </table>


            <table style="width:40%; margin-right:1px">
                <tr>

                    <th>Product name</th>

                </tr>
                <tr v-for="nam in name" v-bind:key="nam">

                    <td>{{nam}}</td>
                </tr>
            </table>

            <table>
                <tr>


                    <th>Quantity</th>
                    <th>Total price</th>
                    <th>Order Date</th>
                    <th>Delivery Date</th>
                </tr>

                <tr v-for="item in product" v-bind:key="item">

                    <td>{{item.quantity}}</td>
                    <td>{{item.total_price}}</td>
                    <td>{{item.order_date}}</td>
                    <td>{{item.delivery_data}}</td>
                </tr>
            </table>

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
                name: [],
                orders: null,
                count: 0,
                order: [],
                product: [],
               

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
           
            getbrandproduct: function (response) {
              
                for (var i = 0; i < response.length; i++) {
                    console.log(response[i]);
                    axios
                        .get('http://localhost/API/api/read_singleproduct.php?ID=' + response[i].product_id)
                        .then(response => (this.checkbrandid(response.data))
                        )


                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)


                }
                console.log(this.product)

            },

            checkbrandid: function (response) {
               
                var brandid = this.x.id;
                console.log(brandid)
                if (response.brand_id == brandid) {
                        this.order.push(response.id);

                    this.name.push(response.name)
                }

                var id = this.order.pop();
                if (id != undefined) {

                    axios
                        .get('http://localhost/API/api/read_order.php?Product_ID=' + id)
                        .then(response => (this.product.push((response.data.data)[0]))
                        )

                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)




                }                 



            },
         


        },
        mounted() {

            var u = localStorage.getItem('users')

            axios
                .get('http://localhost/API/api/read_singleorders.php?Username=' + u)
                .then(response => (this.productname(response.data.data))
                )


                .catch(error => console.log(error))
                .finally(() => this.loading = false)

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

                axios
                    .get('http://localhost/API/api/readorders.php')
                    .then(response => (this.getbrandproduct(response.data.data))

                    )


                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)





            }
            else {
                axios
                    .get('http://localhost/API/api/read_singleorders.php?Username=' + u)
                    .then(response => (this.orders = response.data.data)
                    )


                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                this.count = 0
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
            text-align: left;
            display:flex
        }

            .main .mainsection a {
                color: #dc3545;
                border: 2px solid #043b5f;
                font-size: 20px;
                width: 70px;
                padding: 5px 30px 5px 30px;
                margin-left: 100px;
            }

            .main .mainsection table {
                width: 120%;
            }

                .main .mainsection table tr {
                    border:1px solid #000;
               
                    }

                .main .mainsection table td {
                    border: 2px solid #000;
                    color: #000;
                    height: 50px;
                    text-align: center;
                }

                .main .mainsection table th {
                    border: 2px solid #000;
                    color: #dc3545;
                    height: 50px;
                    text-align: center;
                }
</style>