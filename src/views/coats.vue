<template>
    <div>
        <h1>Coats</h1>
        <div class="row container1">

            <div class="col-md-4 first" v-for="user in all_users" v-bind:key="user" @click="show(user)">
                <h2>{{user['name']}}</h2>

                <img :src="require(`../assets/${user.description}`)" />
                <p class="price">{{user['price']}}</p>
                <p>{{user['color']}}</p>
                <p>{{user['size']}}</p>



                <p><button @click="addcart(user)">add to cart</button></p>


            </div>

        </div>
    </div>

</template>


<script>
    import axios from "axios";


    export default {
        name: 'app',
        data() {
            return {
                loading: false,
                all_users: null,
                a: [],
                c: 0,
                allproductid: null,
                input: {
                    Username: null,
                    Product_id: null,
                    price: null,
                    quantity: null
                }
            }
        },
        mounted() {

            axios
                .get('http://localhost/API/api/read_singlecart.php?Username=' + localStorage.getItem('users'))
                .then(response => (this.getproductid(response.data.data)))
                .catch(error => console.log(error))
                .finally(() => this.loading = false)



        },

        beforeMount() {
            localStorage.setItem('counter', 0)
            localStorage.setItem('product', this.a)
            this.loading = true;

            axios
                .get('http://localhost/API/api/read_Category.php?Category_id=7')
                .then(response => (this.all_users = response.data.data))
                .catch(error => console.log(error))
                .finally(() => this.loading = false)


            this.mounted();

        },
        methods: {

            getImgUrl: function (pic) {

                return require("../assets/" + pic)
            },
            getproductid: function (x) {
                for (var i = 0; i < x.length; i++) {
                    this.a.push(x[i].productid)


                }
                localStorage.setItem('product', this.a)

            },

            addcart: function (user) {
                if (this.a.length == 0) {
                    this.a.push(user.id)
                    localStorage.setItem('product', this.a)
                    localStorage.setItem('counter', parseInt(localStorage.getItem('counter')) + 1)
                    this.input.Username = localStorage.getItem('users');
                    this.input.Product_id = user.id;

                    this.input.quantity = parseInt(1);

                    this.input.price = parseInt(user.price);

                    axios.post("http://localhost/API/api/createcart.php", this.input)

                        .then((result) => {
                            console.log(result.data),
                                localStorage.setItem('count', 1),

                                localStorage.setItem('quantity', this.input.quantity),
                                window.location.reload();
                        })
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)

                }
                else if (this.a.length == 1) {
                    if (this.a[0] == user.id) {

                        this.input.Username = localStorage.getItem('users');
                        this.input.Product_id = user.id;
                        this.input.quantity = parseInt(localStorage.getItem('quantity')) + parseInt(1);

                        localStorage.setItem('product', this.a)
                        this.input.price = parseInt(user.price) * parseInt(this.input.quantity);
                        axios.post("http://localhost/API/api/updatecart.php", this.input)

                            .then((result) => {
                                console.log(result.data),
                                    localStorage.setItem('quantity', this.input.quantity);

                            })
                            .catch(error => console.log(error))
                            .finally(() => this.loading = false)

                    }
                    else {
                        this.a.push(user.id);
                        localStorage.setItem('product', this.a)
                        localStorage.setItem('counter', parseInt(localStorage.getItem('counter')) + 1)
                        this.input.Username = localStorage.getItem('users');
                        this.input.Product_id = user.id;

                        this.input.quantity = parseInt(1);

                        this.input.price = parseInt(user.price);

                        axios.post("http://localhost/API/api/createcart.php", this.input)

                            .then((result) => {
                                console.log(result.data),
                                    localStorage.setItem('count', 1),

                                    localStorage.setItem('quantity', this.input.quantity),
                                    window.location.reload();
                            })
                            .catch(error => console.log(error))
                            .finally(() => this.loading = false)


                    }

                }

                else {
                    while (this.c < this.a.length) {
                        if (this.a[this.c] == user.id) {
                            this.input.Username = localStorage.getItem('users');
                            this.input.Product_id = user.id;
                            this.input.quantity = parseInt(localStorage.getItem('quantity')) + parseInt(1);

                            this.input.price = parseInt(user.price) * parseInt(this.input.quantity);
                            axios.post("http://localhost/API/api/updatecart.php", this.input)

                                .then((result) => {
                                    console.log(result.data),
                                        localStorage.setItem('quantity', this.input.quantity);

                                })
                                .catch(error => console.log(error))
                                .finally(() => this.loading = false)
                            this.c = 0;
                            break;
                        }
                        else {

                            this.c = this.c + 1

                        }


                    }
                    if (this.c == this.a.length) {
                        this.a.push(user.id);
                        localStorage.setItem('product', this.a)
                        localStorage.setItem('counter', parseInt(localStorage.getItem('counter')) + 1)
                        this.input.Username = localStorage.getItem('users');
                        this.input.Product_id = user.id;

                        this.input.quantity = parseInt(1);

                        this.input.price = parseInt(user.price);

                        axios.post("http://localhost/API/api/createcart.php", this.input)

                            .then((result) => {
                                console.log(result.data),
                                    localStorage.setItem('count', 1),

                                    localStorage.setItem('quantity', this.input.quantity),
                                    window.location.reload();
                            })
                            .catch(error => console.log(error))
                            .finally(() => this.loading = false)

                    }


                }



                this.loading = true;

                axios
                    .get('http://localhost/API/api/read_cartproduct.php?Username=' + localStorage.getItem('users') +
                        '&Product_id=' + user.id)
                    .then(response => localStorage.setItem('count', response.data.data.length))
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


                axios
                    .get('http://localhost/API/api/read_cartproduct.php?Username=' + localStorage.getItem('users') +
                        '&Product_id=' + user.id)
                    .then(response =>
                        localStorage.setItem('quantity', (response.data.data)[0].quantity))

                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)


            }




        }

    }

</script>

<style scoped>

    h1 {
        text-align: center;
        margin-top: 50px;
        margin-bottom: 0px;
        background: -webkit-linear-gradient(#fadcda, #dc3545);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        font-size: 60px;
    }

    .container1 {
        width: 100%;
    }

    .col-md-4 {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        max-width: 300px;
        margin: auto;
        text-align: center;
        font-family: arial;
        font-size: 20px;
        margin-top: 50px;
        margin-bottom: 20px;
    }

        .col-md-4 img {
            width: 100%;
        }

    .price {
        color: grey;
        font-size: 22px;
    }

    .col-md-4 button {
        border: none;
        outline: 0;
        padding: 12px;
        color: white;
        background-color: #000;
        text-align: center;
        cursor: pointer;
        width: 100%;
        font-size: 18px;
    }

    .card button:hover {
        opacity: 0.7;
    }
</style>
