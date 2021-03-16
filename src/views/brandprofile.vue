<template>
    <div>
        <br />
        <br />
        <br />
        <br />
        <br />

        <div class="row">
            <div class="left col-lg-4">
                <div class="photo-left">
                    <img class="photo"
                        
                 :src="require(`../assets/${brand.logo}`)"  />
                    <div class="active"></div>
                </div>
                <h4 class="name">{{brand.name}}</h4>
              
         
                <div class="stats row">
                  
                 
                    <div class="stat col-xs-4" style="padding-left: 50px;">
                        <p class="number-stat">{{count}}</p>
                        <p class="desc-stat">Uploads</p>
                    </div>
                </div>
                <p class="desc">
                  {{brand.about}}       </p>
                <div class="social">
                    <i class="fa fa-facebook-square" aria-hidden="true"></i>
                    <i class="fa fa-twitter-square" aria-hidden="true"></i>
                    <i class="fa fa-pinterest-square" aria-hidden="true"></i>
                    <i class="fa fa-tumblr-square" aria-hidden="true"></i>
                </div>
            </div>
            <div class="right col-lg-8">
                <ul class="nav">
                    <li style="font-size:30px">  <b>Collections</b></li>
                </ul>
     
                <div  class="row gallery">
                    
                    <div class="col-md-4" v-for="product in brand_product" v-bind:key="product">
                        <h6>{{product.name}}</h6>

                        <img :src="require(`../assets/${product.description}`)" />
                    </div>
                   
                </div>
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
           brand_product:null,
                count: 0,
                brand:null,
            }
        },
      

        beforeMount() {
         
            this.loading = true;

            var x=localStorage.getItem('clickbrand')
            axios
                .get('http://localhost/API/api/read_singleebrand.php?Name=' + x)
                .then(response => (this.getid(response.data)))
                .catch(error => console.log(error))
                .finally(() => this.loading = false)




        },
        methods: {
            getid: function (response) {
                this.brand = response;
                console.log(response.id)
                axios
                    .get('http://localhost/API/api/read_brand.php?Brand_ID=' + response.id)
                    .then(response => (this.brand_product = response.data.data)
                )
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                axios
                    .get('http://localhost/API/api/read_brand.php?Brand_ID=' + response.id)
                    .then(response => (this.count = response.data.data.length)
                    )
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
             

            },
        





        }

    }

</script>


<style scoped>
    html,
    body {
        background: #efefef;
        font-family: "Arial";
    }

    .container {
        max-width: 1250px;
        margin: 30px auto 30px;
        padding: 0 !important;
        width: 90%;
        background-color: #fff;
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1), 0 3px 6px rgba(0, 0, 0, 0.1);
    }
    .row{
        width:100%
    }
    main {
        padding: 20px 20px 0px 20px;
    }

    .left {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }

    .photo {
        width: 200px;
        height: 200px;
        margin-top: -120px;
        border-radius: 100px;
        border: 4px solid #fff;
    }

    .active {
        width: 20px;
        height: 20px;
        border-radius: 20px;
        position: absolute;
        right: calc(50% - 70px);
        top: 75px;
        background-color: #ffc107;
        border: 3px solid #fff;
    }

    @media (max-width: 990px) {
        .active {
            right: calc(50% - 60px);
            top: 50px;
        }
    }

    .name {
        margin-top: 20px;
        font-family: "Open Sans";
        font-weight: 600;
        font-size: 18pt;
        color: #777;
    }

    .info {
        margin-top: -5px;
        margin-bottom: 5px;
        font-family: "Montserrat", sans-serif;
        font-size: 11pt;
        color: #aaa;
    }

    .stats {
        margin-left:300px;
        margin-top: 25px;
        text-align: center;
        padding-bottom: 20px;
        border-bottom: 1px solid #ededed;
        font-family: "Montserrat", sans-serif;
    }

    .number-stat {
        padding: 0px;
        font-size: 14pt;
        font-weight: bold;
        font-family: "Montserrat", sans-serif;
        color: #aaa;
    }

    .desc-stat {
        margin-top: -15px;
        font-size: 10pt;
        color: #bbb;
    }

    .desc {
        text-align: center;
        margin-top: 25px;
        margin: 25px 40px;
        color: #000;
        font-size: 11pt;
        font-family: "Open Sans";
        padding-bottom: 25px;
        border-bottom: 1px solid #ededed;
    }

    .social {
        margin: 5px 0 12px 0;
        text-align: center;
        display: inline-block;
        font-size: 20pt;
    }

        .social i {
            cursor: pointer;
            margin: 0 15px;
        }

            .social i:nth-child(1) {
                color: #4267b2;
            }

            .social i:nth-child(2) {
                color: #1da1f2;
            }

            .social i:nth-child(3) {
                color: #bd081c;
            }

            .social i:nth-child(4) {
                color: #36465d;
            }

    .right {
        padding: 0 25px 0 25px !important;
    }

    .nav {
        display: inline-flex;
    }

        .nav li {
            margin: 40px 30px 0 10px;
            cursor: pointer;
            font-size: 13pt;
            text-transform: uppercase;
            font-family: "Montserrat", sans-serif;
            font-weight: 500;
            color: #888;
        }

            .nav li:hover,
            .nav li:nth-child(1) {
                color: #999;
                border-bottom: 2px solid #999;
            }

    .AddProduct {
        position: absolute;
        right: 20%;
        top: 35px;
        font-size: 11pt;
        background-color: #ff9da6;
        color: #fff;
        padding: 8px 15px;
        cursor: pointer;
        transition: all 0.4s;
        font-family: "Montserrat", sans-serif;
        font-weight: 400;
    }

    .follow {
        position: absolute;
        right: 8%;
        top: 35px;
        font-size: 11pt;
        background-color: #ff9da6;
        color: #fff;
        padding: 8px 15px;
        cursor: pointer;
        transition: all 0.4s;
        font-family: "Montserrat", sans-serif;
        font-weight: 400;
    }

    .AddProduct:hover {
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.2), 0 0 15px rgba(0, 0, 0, 0.2);
    }

    .follow:hover {
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.2), 0 0 15px rgba(0, 0, 0, 0.2);
    }

    @media (max-width: 990px) {
        .nav {
            display: none;
        }

        .follow {
            width: 50%;
            margin-left: 25%;
            display: block;
            position: unset;
            text-align: center;
        }

        .AddProduct {
            width: 50%;
            margin-left: 25%;
            display: block;
            position: unset;
            text-align: center;
        }
    }

    .gallery {
        margin-top: 35px;
    }

        .gallery div {
            margin-bottom: 30px;
        }

        .gallery img {
            box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1), 0 3px 6px rgba(0, 0, 0, 0.1);
            width: auto;
            height: auto;
            cursor: pointer;
            max-width: 100%;
        }
</style>