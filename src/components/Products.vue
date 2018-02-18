<template>   
    <div class="container mt-5 py-2">
  		        <h1 class="my-2">Products</h1>
       <div class="row">
           <div v-for="product in products" :key="product.id" class="col-sm-6 col-md-4 p-2">
               <single-product 
               		:product="product"
               		@add-to-cart="onAddToCart"
              ></single-product>
           </div>
       </div>
   </div>
</template>   

<script>
    import SingleProduct from "./SingleProduct.vue"
    export default{
        	props: ['products'],
        components: {
            SingleProduct
        },
        methods: {
            onAddToCart(id) {
        		       this.$emit("add-to-cart", id);
        	    }
        }
    }
</script>
