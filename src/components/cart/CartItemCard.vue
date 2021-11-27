<template>
    <div class="cart-item-card">
        <div class="header">
            <img class="img" :src= "item.img">
            <h3>{{ item.name }}</h3>
            <h4>In Cart: {{ item.quantity }}</h4>
            <h4>Price: {{ item.price }}</h4>
            <h4>Total Cost: {{ item_cost.toFixed(2) }} PHP</h4>
            <div class="button-container">
                <button class="remove" @click.prevent="removeFromCart()">Remove</button>
                <button class="add" @click.prevent="addToCart()">Add</button>
            </div>
        </div>
        
        <p>{{ description }}</p>
    </div>
</template>

<script>
    export default {
        props: ['item'],
        methods: {
            addToCart() {
                this.$store.commit('addToCart', this.item)
            },
            removeFromCart() {
                this.$store.commit('removeFromCart', this.item)
            }
        },
        computed: {
            description() {
                return this.item.description.substring(0, 120)
            },
            item_cost() {
                return this.item.price * this.item.quantity
            }
        }
    }
</script>

<style lang="scss">
    .cart-item-card {
        width: 90%;
        margin: 5%;
        background-color: white;
        box-shadow: 0 0 5px gray;
        border-radius: 5px;
        padding: 10px;
        text-align: left;

        .header {
            display: flex;
            justify-content: space-around;
        }

        img.img{
            width:15%;
        }
        .button-container {
            button {
                width: 150px;
                border: none;
                padding: 10px;
                border-radius: 5px;
                margin: 0 5px 50px 5px;
                cursor: pointer;
            }

            button.remove {
                
            }

            button.add {

            }
        }
    }
</style>