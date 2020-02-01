<template>
  <div>
    <div v-if="emptyCart">
      <h6>Your bag is empty</h6>
      <shopping-bag-black class="no__cart" />
    </div>
    <div v-else class="cart__wrapper" v-for="cartItem in cartItems.cartItem" :key="cartItem.itemId">
      <p>{{ cartItem.title }}</p>
      <div class="cart__wrapper-content">
        <div class="cart__wrapper-image">
          <img :src="cartItem.itemPhoto" alt="">
          <p>{{ cartItem.variantId }}</p>
        </div>
        <div class="cart__wrapper-quantity">
          <button class="quantity__btn">
            -
          </button>
          <span class="cart__quantity">{{ cartItem.quantity }}</span>
          <button class="quantity__btn">
            +
          </button>
        </div>
        <div class="cart__wrapper-price">
          {{ cartItem.price | toUSD }}
        </div>
      </div>
    </div>
    <div class="cart__wrapper-total"><span>Total:</span> {{ cartItems.totalPrice | toUSD }}</div>
    <el-button round class="black checkout">
      checkout
    </el-button>
    <el-button round class="no__cart-btn" @click="closeCartDrawer">
      Browse Products
    </el-button>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import ShoppingBagBlack from '../icons/ShoppingBagBlack'

export default {
  components: {
    ShoppingBagBlack
  },

  props: {
    emptyCart: {
      type: Boolean,
      required: true
    }
  },

  computed: {
    ...mapGetters(['cartItems'])
  },

  methods: {
    closeCartDrawer() {
      this.$emit('close-cart-drawer', false)
    }
  }
}
</script>

<style lang="scss">
.no__cart {
  width: 100px;
  position: absolute;
  top: 40%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);

  &-btn {
    position: absolute;
    bottom: 0;
    margin: 0 0 50px;
    min-height: 40px;
    width: 100%;
  }
}

.cart__wrapper {
  font-size: 0.7rem;
  border-bottom: 1px solid black;
  margin-bottom: 10px;
  padding-bottom: 5px;
}

.cart__wrapper-content{
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 1fr 2fr 1fr;
}

.cart__wrapper-price{
  display: flex;
  justify-content: flex-end;
  font-weight: 600;
  align-items: center;
}

.cart__wrapper-quantity {
  display: grid;
  justify-items: center;
  grid-template-columns: 1fr 2fr 1fr;
  align-items: center;
}

.cart__wrapper-total{
  display: flex;
  justify-content: flex-end;
  margin: 20px 0px;
  font-weight: 600;
}

.el-drawer__body {
  width: 25.36111vw !important;
}

.el-button.checkout{
  display: block;
  float: right;
}

.quantity__btn{
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.2em;
}

.quantity__btn{
  border: 1px solid black;
    height: 20px;
   padding: 0 6px;
}
</style>