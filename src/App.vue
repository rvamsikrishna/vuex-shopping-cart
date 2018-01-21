<template> 
    <div>
  	     <navbar></navbar>
  		    <products></products>
  		    
  		    <cart></cart>
  		    
  		    <toast :show="toast.show" :text="toast.text" @hide-toast="hideToast"></toast>
  	 </div>  
</template>

<script>
    import Navbar from './components/Navbar.vue'
    import Products from './components/Products.vue'
    import Cart from './components/Cart.vue'
    import Toast from './components/Toast.vue'
    
  	  export default {
  		     data(){
  			        return{
  			
  			        };
  		      },
  		      components:{
  			        Navbar,
  			        Products,
  			        Cart,
  			        Toast
  		      },
  		      computed: {
  		          toast() {
  		              return this.$store.getters.toast;
  		          }
  		      },
  		      methods: {
  		          hideToast() {
  		              this.$store.commit("hideToast");
  		          }
  		      }
 	    }   
</script>

<style scoped>

</style>
