<template>
    <div class="row">
        <div class="card text-white bg-dark mb-3">
            <div class="card-columns">
                <h3 class="card-columns">
                {{ stock.name }}
                <small>(Price: {{ stock.price }})</small>
                </h3>
                <h4>(Quantity: {{ stock.quantity }})</h4>
            </div>
            <div class="card-columns">
                <div>
                    <input 
                            type="number" 
                            class="form-control" 
                            placeholder="Quantity"
                            v-model.number="quantity"
                            :class="{danger: insufficientQuantity}"
                            />
                </div>
                <div>
                    <button 
                            class="btn btn-success"
                            @click="sellStock"
                            :disabled="insufficientQuantity || quantity <= 0"
                            >{{ insufficientQuantity ? 'Not enough stocks' : 'Sell'}}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .danger {
        border: 1px solid red;
    }
</style>

<script>
    import {mapActions} from 'vuex';
    export default {
        props: ['stock'],
        data() {
            return {
                quantity: 0
            }
        },
        computed: {
            insufficientQuantity() {
                return this.quantity > this.stock.quantity;
            }
        },
        methods: {
            ...mapActions({
                placeSellOrder: 'sellStock'
            }),
            sellStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                this.placeSellOrder(order);
                this.quantity = 0;
            }
        }
    }
</script>