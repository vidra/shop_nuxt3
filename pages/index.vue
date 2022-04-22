<template>
<div class="container">
        <div class="row">
            <div v-for="(product, index) in products"
                  :key="'product-'+ index"
                   class="col-md-4">
                <div class="card mb-3">
                    <img :src="product.photoURL" class="card-img-top">
                    <div class="card-body">
                        <h5 class="card-title">
                            {{ product.name }}
                        </h5>
                        <p class="card-text">
                            {{ product.description }}
                        </p>
                        <div class="d-grid">
                            <button @click="addToCart(product)" class="btn btn-outline-primary">
                                Add to cart
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
<ShoppingCart />
    </div>
</template>

<script >
export default {
data() {
return {
products: [
{
uuid: '344-33-20',
name: 'Camera0',
description: 'Lorem ipsum dolor sit amet',
price: 950,
photoURL: 'https://picsum.photos/500/500/?image=54'
},
{
uuid: '344-33-21',
name: 'Camera1',
description: 'Lorem ipsum dolor sit amet',
price: 950,
photoURL: 'https://picsum.photos/500/500/?image=54'
},
{
uuid: '344-33-22',
name: 'Camera2',
description: 'Lorem ipsum dolor sit amet',
price: 950,
photoURL: 'https://picsum.photos/500/500/?image=54'
}


],
shoppingCart: []
}
},
 mounted() {
        this.shoppingCart = JSON.parse(localStorage.getItem('shoppingCart') || "[]")
    },
    watch: {
        shoppingCart: {
            handler(newValue) {
                localStorage.setItem('shoppingCart', JSON.stringify(newValue));
            }, deep: true
        }
    },
methods: {
        addToCart(product) {
            let exists = false;

            for (const cartItem of this.shoppingCart) {
                if (cartItem.uuid === product.uuid) {
                    cartItem.amount = cartItem.amount + 1;
                    exists = true;
                    break;
                }
            }
            if (!exists) {
                this.shoppingCart.push({
                    ...product,
                    amount: 1,
                })
}
},
}
}

</script>
