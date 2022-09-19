<template>
    <div class="">
        <div
            class="flex items-center space-x-6 item-container"
            :class="
                (index % 2 === 0 ? 'bg-grey' : '',
                dataItem.stock === '0' ? 'relative' : '')
            "
        
        >
 
            <div class="w-full">
                <div class="cart-level-1">
                    <span class="text-light-grey"
                        >No. SKU 1912</span
                    >
                    <p
                        class="text-center flex items-center justify-end text-secondary f-10 mb-0"
                    >
                        <s>
                            IDR
                        20000
                        </s>
                    </p>
                </div>
                <div class="cart-level-2">
                    <span class="d-block mb-0">top</span>

                    <div  class="qty">
                        <div class="form-step-input">
                            <button
                                type="button"
                                class="form-step-minus form-step-counter"
                                :disabled="isLoading"
                                :style="{
                                    opacity: isLoading ? 0.4 : 1
                                }"
                                @click.stop="handleMinus"
                            >
                                -
                            </button>
                            <input
                                ref="qtyOrder"
                                :value="qtyProduct"
                                type="number"
                                step="1"
                                min="1"
                                name="qtyOrder"
                                @shortkey="$refs.qtyOrder.focus()"
                                @change="addQtyChange($event)"
                            />
                            <button
                                type="button"
                                class="form-step-plus form-step-counter"
                      
            
                                @click.stop="handlePlus"
                            >
                                +
                            </button>
                        </div>
        
                    </div>


                    <section >
                        <div
                            class="price text-center flex items-center justify-end text-semibold text-primary f-20 mb-0"
                        >

                            <div>
                                IDR
                              400000
                            </div>
                        </div>
                    </section>
                </div>


               
                    <button
                        class="btn-icon btn-icon--transparent"
                        :class="
                            dataItem.stock === '0' ? 'absolute right-20' : ''
                        "
                        @click.stop="handleDelete"
                    >
                        <i class="icon-trash"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'ItemListCheckout',
    props: {
        dataItem: { type: Object, require: true, default: Object },
        qty: { type: Number, require: true, default: Number },
        index: { type: Number, require: true, default: Number },
    },
    data() {
        return {
            qtyProduct: 1,
            totalPrice: 1000,
            isOpenModal: false,
            activeModal: '',
            orderItemsId: null,
            couponCode: null,
            isAlertExistModal: false,
            isAlertModalMessage: '',
            editPrice: false,
            username: '',
            password: '',
            isLoading: false,
            stock: '',
            addProcuctAuth: false,
            handleStatus: 'plus'
        }
    },
    computed: {
 
    },
    methods: {
    addQtyChange(event) {
            const { value } = event.target

                this.qtyProduct = parseInt(value)

        },
    }
}
</script>

<style scoped>
.shortcut-parent {
    padding-right: 0;
}
.shortcut-label {
    right: 80%;
}
.lds-ellipsis {
    height: max-content;
    position: absolute;
    right: 0;
}
.container-edit-price {
    background-color: #fff;
    height: 32px;
    border-radius: 7px;
}
 .container-edit-price  input {
        height: 100%;
        display: flex;
        width: 100%;
        text-align: right;
        border: 1px solid #cdd3da;
        border-radius: 4px;
        color: #ff6600;
        font-size: 1.25em;
        font-weight: 500;
    }
.out-of-stock {
    position: absolute;
    height: 100%;
    width: 90%;
    background-color: rgba(247, 247, 247, 0.5);
}
.price {
    position: relative;
}
.edit-price {
    position: absolute;
    right: 80%;
    display: none;
    color: #333;
}

.icon {
    background-color: rgba(228, 228, 228, 0.671);
    padding: 0.2em;
    border-radius: 50%;
    height: 25px;
}

.bg-grey {
    background-color: rgba(238, 238, 238, 0.438);
}

.cart-level-1 {
    display: flex;
    justify-content: space-between;
    margin-bottom: 2px;

}
   .cart-level-1 span {
        font-size: 16px;
    }

 .qty   .form-step-input {
        width: max-content;
    }
.qty {
    position: relative;
    display: flex;

    flex-direction: column;
}
    .article-stock {
        position: absolute;
        top: 100%;
        left: 8%;
    }
  .cart-level-2  span {
        font-weight: 600;
        font-size: 20px;
    }

.cart-level-2 {
    display: flex;
    align-items: center;
    margin-bottom: 2px;

}

         .cart-level-2:first-child {
            flex: 1 50%;
        }

         .cart-level-2:nth-child(2) {
            flex: 0 100px;
        }

         .cart-level-2:last-child {
            flex: 0 25%;
        }

.cart-level-3 {
    display: flex;
    margin-bottom: 6px;
}
     .cart-level-3 span {
        font-size: 12px;
    }

.cart-level-4 {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 2px;
    font-size: 16px;
}

.item-container {
    padding: 0.5em 1.5em;
    border-bottom: 1px solid rgba(182, 181, 181, 0.5);
    background: #f8f8f8;

}
    .item-container:hover {
        background: #ffece7;
        cursor: pointer;
    }
    .item-container:hover .edit-price {
        display: block;
    }
</style>
