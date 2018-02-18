<template> 
    <div>
  	     <navbar></navbar>
  		    <products 
  		    	    :products="products"
  		    	    @add-to-cart="addToCart"
  		    ></products>
  		    
  		    <cart 
  		        :cart="cart"
  		        @increase-in-cart="addToCart"
  		        @remove-from-cart="removeFromCart"
  		        @delete-from-cart="deleteFromCart"
  		    ></cart>
  		    
  		    <toast :show="toast.show" :text="toast.text" @hide-toast="hideToast"></toast>
  	 </div>  
</template>

<script>
    import Navbar from './components/Navbar.vue'
    import Products from './components/Products.vue'
    import Cart from './components/Cart.vue'
    import Toast from './components/Toast.vue'
    import myApi from './myApi'
    
  	  export default {
  		     data(){
  			        return{
  						         products: [],
  						         cart: [],
  						         toast: {
  							            show :false,
  							            text: ''
  						         }
  			        };
  		      },
  		      components:{
  			        Navbar,
  			        Products,
  			        Cart,
  			        Toast
  		      },
  		      created() {
  		      	    //simulating a fake ajax request to fetch products from database
            	 myApi.getProducts().then((products) => {
                
                	//setting the products recieved from response to products property in data option
					           this.products = products;
               	 this.showToast("products loaded");
				        });
  		      },
  		      methods: {
  		      	  addToCart(id) {
  		      	  	     //find the product in the products list
                let product = this.products.find((product) => product.id === id);
                
                //find the product in the cart list
                let cartProduct = this.cart.find((product) => product.id === id);
    
                if (cartProduct) {
                    //product already present in the cart. so increase the quantity
                    cartProduct.quantity++;
                } else {
                    this.cart.push({
                        // product newly added to cart
                        ...product,
                        stock: product.quantity,
                        quantity: 1,
                    });
                }
                //reduce the quantity in products list by 1
                product.quantity--;
                this.showToast("added to cart");
  		      	  },
  		      	  removeFromCart(id) {
  		      	      //find the product in the products list
                let product = this.products.find((product) => product.id === id);
                
                //find the product in the cart list
                let cartProduct = this.cart.find((product) => product.id === id);
    
                cartProduct.quantity--;
                
                //Add back the quantity in products list by 1
                product.quantity++;
                this.showToast("removed from cart");
  		      	  },
  		      	  deleteFromCart(id) {
  		      	      //find the product in the products list
                let product = this.products.find((product) => product.id === id);
                
                //find the product index in the cart list
                let cartProductIndex = this.cart.findIndex((product) => product.id === id);
                
                
                //set back the quantity of the product to intial quantity
                product.quantity = this.cart[cartProductIndex].stock;
                
                // remove the product from the cart
                this.cart.splice(cartProductIndex, 1);
                this.showToast("deleted from cart");
  		      	  },
  		      	  showToast(text) {
  		      	  	    this.toast.show = true;
					          this.toast.text = text;
  		      	  },
  		        hideToast() {
			           	this.toast.show = false;
					         this.toast.text = "";
  		          }
  		      }
 	    }   
</script>

<style scoped>

</style>
