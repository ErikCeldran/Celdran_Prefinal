<template>
    <div class="cart-item-card">
        <h3>Cart Total: {{ cart_total.toFixed(2) }} PHP</h3>
        <h4>Add Coupon Code: </h4>
        <input type="string" v-model="coupon"/><br>
        <div class="coupon_total" v-if="coupon_total">
            <h3>New Total: {{ coupon_total.toFixed(2) }} PHP</h3>
        </div>
        <h4>Enter Money: </h4>
        <input type="number" v-model="count"/><br>
        <button class="view-product-button" @click.prevent="paymentCheck()">Pay</button>
    </div>
</template>

<script>
    export default {
        data() {
            return{
                count: 0,
                coupon: ""
            }
        },
        computed: {
            cart_total() {
                return this.$store.getters.cartItems.reduce((a, b) => a + (b.price * b.quantity), 0)
            },
            payment() {
                return this.count - this.coupon_total
            },
            coupon_total() {
                if(this.coupon === "menu50"){
                    return this.cart_total * 0.5
                } else if(this.coupon === "menu20"){
                    return this.cart_total * 0.8
                } else if(this.coupon === "menu10"){
                    return this.cart_total * 0.9
                } else if(this.coupon === "menu200flat" && this.cart_total >= 1000 ){
                    return this.cart_total - 200
                } else {
                    return this.cart_total
                }
            }
        },
        methods: {
            paymentCheck() {
                if (this.payment >= 0){
                    alert("Successful Purchase")
                    console.log('flushing cache...');
                    localStorage.clear();
                    window.location.reload(true);
                } else {
                    alert("Invalid Input, Please check amount again.")
                } 
            },
        }
        
    }
</script>