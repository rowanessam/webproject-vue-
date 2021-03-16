<template>
  <div>
    <div class="container">
      <h1>Shopping Cart</h1>
      <div id="alerts"></div>
      <div v-if="this.y==0" class="productcont3">

       


          <button class="but" @click="changey()">Go to checkout</button>
      </div>




      <div v-else class="cart-container">




          <h2>Cart</h2>

          <div class="carttable">
              <table id="table3" >
                  <thead>
                      <tr>
                          <th><strong>image</strong></th>

                      </tr>
                  </thead>
                  <tbody  id="carttable">

                      <tr v-for="pimg in img" v-bind:key="pimg">

                          <td >
                              <img :src="require(`../assets/${pimg}`)" style="width:50px; height:51px " />
                          </td>
                          <br />
                      </tr>


                  </tbody>
              </table>




              <table id="table1">
                  <thead>
                      <tr>
                          <th><strong>Product</strong></th>

                      </tr>
                  </thead>
                  <tbody id="carttable">

                      <tr v-for="name in pname" v-bind:key="name">

                          <td  style="margin:100px; padding:18px">{{name}}</td>
                          <br />
                      </tr>


                  </tbody>
              </table>
              <table id="table2">
                  <thead>
                      <tr>
                          <th><strong>Quantity</strong></th>
                          <th><strong>Price</strong></th>
                      </tr>
                  </thead>
                  <tbody id="carttable">

                      <tr v-for="user in all_users" v-bind:key="user">

                          <td style="margin:100px; padding:18px"> {{user.quantity}}</td>

                          <td style="margin:100px; padding:18px">{{user.price}}</td>
                      </tr>


                  </tbody>
              </table>
          </div>

          <hr />
          <table id="carttotals">
              <tr>
                  <td><strong>Items</strong></td>

                  <td>x <span id="itemsquantity">{{tquantity}}</span></td>

              </tr>


              <tr>
                  <td><strong>shipping </strong></td>

                  <td>$<span id="total">{{shipping}}</span></td>

              </tr>
              <tr>
                  <td><strong>Total</strong></td>

                  <td>$<span id="total">{{tprice}}</span></td>
              </tr>

          </table>
          



          <div class="cart-buttons">
              <div>
                  <h5 style="color: #c72b6e;">It will arrive By {{afterweek}}</h5>
              </div>
              <div>
                  <button id="emptycart" @click="emptyall()">Empty Cart</button>
                  <button id="checkout" @click="checkout()">Checkout</button>
              </div>

          </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
@import url("https://fonts.googleapis.com/css?family=Quicksand:400,700");
*,
::before,
::after {
  box-sizing: border-box;
}
body {
  font-family: "Quicksand", sans-serif;
  text-align: center;
  line-height: 1.5em;
  /*   background:#E0E4CC; */
  background: #fadcda;
  background: -moz-linear-gradient(
    -45deg,
    #fadcda 0%,
    #fadcda 25%,
    #e0e4cc 46%,
    #e0e4cc 54%,
    #c72b6e 75%,
    #c72b6e 100%
  );
  background: -webkit-linear-gradient(
    -45deg,
    #fadcda 0%,
    #fadcda 25%,
    #e0e4cc 46%,
    #e0e4cc 54%,
    #c72b6e 100%
  );
  background: linear-gradient(
    135deg,
    #fadcda 0%,
    #fadcda 25%,
    #e0e4cc 46%,
    #e0e4cc 54%,
    #f38630 75%,
    #fa6900 100%
  );
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#69d2e7', endColorstr='#fa6900',GradientType=1 );
}
hr {
  border: none;
  background: #e0e4cc;
  height: 1px;
  /*   width:60%;
  display:block;
  margin-left:0; */
}
.container {
  max-width: 800px;
  margin: 1em auto;
  background: #fff;
  padding: 30px;
  border-radius: 5px;
  
}
.btn{
   font-size:10px;
   margin-left:100px;
   margin-bottom:10px
}
.productcont {
  display: flex;


}
    .productcont3 {
        display: flex;
        flex-direction:column
    }
        .productcont3 .but{
            margin:auto;
            margin-top:50px;
            font-size:20px;
            width:50%;
           
        }

        .productcont3 .but:focus {

            outline:0px;
            border:0px;

        }

            .product {
            padding: 1em;
            border: 1px solid #e0e4cc;
            margin-right: 1em;
            border-radius: 5px;
        }
.cart-container {
  border: 1px solid #e0e4cc;
  border-radius: 5px;
  margin-top: 1em;
  padding: 1em;
}
button,
input[type="submit"] {
  border: 1px solid #c72b6e;
  color: #fff;
  background: #c72b6e;
  padding: 0.6em 1em;
  font-size: 1em;
  line-height: 1;
  border-radius: 1.2em;
  transition: color 0.2s ease-in-out,
   background 0.2s ease-in-out,
    border-color 0.2s ease-in-out;
}

button:hover,
button:focus,
button:active,
input[type="submit"]:hover,
input[type="submit"]:focus,
input[type="submit"]:active {
  background: #fadcda;
  border-color: #fadcda;
  color: #000;
  cursor: pointer;
}
table {
  margin-bottom: 1em;
  border-collapse: collapse;
}
table td,
table th {
  text-align: left;
  padding: 0.25em 1em;
  border-bottom: 1px solid #e0e4cc;
}
#carttotals {
  margin-right: 0;
  margin-left: auto;
}
.cart-buttons {
  width: auto;
  margin-right: 0;
  margin-left: auto;
  display: flex;

  justify-content:space-between;
  padding: 1em 0;
}
#emptycart {
  margin-right: 1em;
}
table td:nth-last-child(1) {
  text-align: right;
}
.message {
  border-width: 1px 0px;
  border-style: solid;
  border-color: #fadcda;
  color: #fadcda;
  padding: 0.5em 0;
  margin: 1em 0;
}

.carttable{
    display:flex;

}
</style>

<script>

    import axios from "axios";
    export default {
        name: 'app',
        data() {
            return {
                len:0,
                loading: false,
                all_users: null,
                cart: null,
                pname: [],
                img:[],
                y: 1,
                tprice: 0,
                tquantity: 0,
                today: 0,
                afterweek:0,
                quantity : [],
                i:[],
                j: 0,
               shipping:0,
              input: {
                    Username: null,
                    Product_id: null,
                    price: null,
                    quantity: null
                },
                input1:{
                    ID:null
                },
                input2: {
                    Product_ID: null,
                    Total_Price: null,
                    Delivery_Data: null,
                    Order_Date: null,
                    Quantity: null,
                    Username: null
                },

                input3: {
                    ID: null,
                    Category_id: null,
                    Colors: null,
                    Sizes: null,
                    Price: null,
                    Brand_ID: null,
                    Description: null,
                    Name: null,
                    quantity:null,


                },
            }

        },
       
        methods: {
            tdate: function () {

                this.today = new Date();
                this.afterweek = new Date();
                var dd = this.today.getDate();
                var mm = this.today.getMonth() + 1; //As January is 0.
                var yyyy =this.today.getFullYear();
                if (dd < 10) dd = '0' + dd;
                if (mm < 10) mm = '0' + mm;

                this.today = mm + "-" + dd + "-" + yyyy;
                
                this.afterweek.setDate(this.afterweek.getDate() + 7);
                var dd1 = this.afterweek.getDate();
                var mm1 = this.afterweek.getMonth() + 1; //As January is 0.
                var yyyy1 = this.afterweek.getFullYear();
                if (dd1 < 10) dd1 = '0' + dd1;
                if (mm1 < 10) mm1 = '0' + mm1;

                this.afterweek =mm1 + "-" + dd1 + "-" + yyyy1;






            },


            checkout: function () {
                  var i = this.all_users.length - 1;
                while (i > -1) {
                    this.input2.Username = localStorage.getItem('users');
                    this.input2.Product_ID = this.all_users[i].productid;
                    this.input2.Total_Price = this.all_users[i].price;
                    this.input2.Quantity = this.all_users[i].quantity;
                    this.input2.Order_Date = this.today;
                    this.input2.Delivery_Data = this.afterweek;
                 
                    axios.post("http://localhost/API/api/createorders.php", this.input2)
                        .then((result) => 
                            console.log(result.data)
                              
                        )
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)
                    this.i.push(this.all_users[i].id)
                  
                    axios
                        .get('http://localhost/API/api/read_singleproduct.php?ID=' + this.all_users[i].productid)
                        .then(response => (this.qq(response.data)))
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)


              
                    i=i-1;
                    


                }

           
           
                
                this.$router.push({ name: 'Home' })
                window.location.reload()   
            },

            qq: function (q) {
              
                axios
                    .get('http://localhost/API/api/read_cartproduct.php?Username=' + localStorage.getItem('users') +
                        '&Product_id=' + q.id)
                    .then(response => this.quan((response.data.data)[0].quantity, q))
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
               
               
               

                //var i = this.all_users.length - 1;
               //while (i > -1) {



                 //   i--;
               // }



            },
            quan: function (quantity, q) {
                var x = q;
                this.input3.ID = x.id;
                this.input3.Category_id = x.category_id;
                this.input3.Brand_ID = x.brand_id;
                this.input3.Colors = x.color;
                this.input3.Sizes = x.size;
                this.input3.Description = x.description;
                this.input3.Name = x.name;
                this.input3.Price = x.price;
             
                this.input3.quantity = parseInt(x.quantity) - parseInt(quantity)

                  axios.post("http://localhost/API/api/updateproduct.php", this.input3)

                      .then((result) => {
                          console.log(result.data)
                      })
                       .catch(error => console.log(error))
                       .finally(() => this.loading = false)
                console.log(this.input3.ID)
                

                this.input1.ID = this.i.pop();

                console.log(this.input1)  
                    axios.post("http://localhost/API/api/deletecart.php", this.input1)
                        .then((result) => {
                            console.log(result.data)

                        })
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)

             
            },




            emptyall: function () {
                var i = this.all_users.length-1
                while (i > -1) {
                    this.remove(this.all_users[i])
                    i--;

                }


                this.$router.push({ name: 'Home' })
            },
            changey: function () {
                this.y = 1;
                console.log(this.all_users.length)
                for (var i = 0; i < this.all_users.length; i++) {
                    this.tquantity = parseInt(this.tquantity) + parseInt(this.all_users[i].quantity)

                    this.tprice = parseInt(this.tprice) + parseInt(this.all_users[i].price)
                    this.shipping = parseInt(parseInt(this.tprice) * (5 / 100));
                    this.tprice = this.tprice + this.shipping;

                    axios
                        .get('http://localhost/API/api/read_singleproduct.php?ID=' + this.all_users[i].productid)
                        .then(response => (this.pname.push(response.data.name)))
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)
                }





            },
            increase: function (user) {
                console.log(user)
                this.input.Username = localStorage.getItem('users');
                this.input.Product_id = user.productid;
                console.log(this.input)

                var len = parseInt(user.price) / parseInt(user.quantity)
                console.log(len)

                this.input.quantity = parseInt(user.quantity) + 1;
                console.log(this.input.quantity)
                this.input.price = parseInt(user.price) + parseInt(len)
                axios.post("http://localhost/API/api/updatecart.php", this.input)
                    .then((result) => {
                        console.log(result.data)

                    })
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                window.location.reload()


            },
            decrease: function (user) {
                this.input.Username = localStorage.getItem('users');
                this.input.Product_id = user.productid;
                console.log(this.input)

                var len = parseInt(user.price) / parseInt(user.quantity)
                console.log(len)

                this.input.quantity = parseInt(user.quantity) - 1;
                console.log(this.input.quantity)
                this.input.price = parseInt(user.price) - parseInt(len)
                axios.post("http://localhost/API/api/updatecart.php", this.input)
                    .then((result) => {
                        console.log(result.data)

                    })
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                window.location.reload()


            },
            remove: function (user) {
                this.input1.ID= user.id;
                console.log(this.input1.ID)
                axios.post("http://localhost/API/api/deletecart.php", this.input1)
                    .then((result) => {
                        console.log(result.data)

                    })
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                window.location.reload()
            },
            select: function (user) {
                this.all_users = user;
                var i = this.all_users.length - 1;
                while (i > -1) {
                 
                  

                    axios
                        .get('http://localhost/API/api/read_singleproduct.php?ID=' + this.all_users[i].productid)
                        .then(response => (this.img.push(response.data.description)))
                        .catch(error => console.log(error))
                        .finally(() => this.loading = false)



                    i = i - 1;



                }


            }

        },
        beforeMount() {
            this.y = 0;
            this.loading = true;
            axios
                .get('http://localhost/API/api/read_singlecart.php?Username=' + localStorage.getItem('users'))
                .then(response => (this.select(response.data.data)))
                .catch(error => console.log(error))
                .finally(() => this.loading = false)
            console.log(this.len)
            this.tdate()
          
        },
    };

</script>