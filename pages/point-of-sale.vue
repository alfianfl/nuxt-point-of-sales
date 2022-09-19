<template>
  <div class="grid-container">
    <div class="grid-container-div1">
      <!-- <InputSKU
                ref="skuComp"
                :products="products || []"
                @valueSKUChange="valueSKUChange"
                @valueServiceChange="valueServiceChange"
                @loading="loading"
            /> -->
      <!-- loader -->
      <div v-if="isValueSKU !== '' && isLoading === true" class="lds-ellipsis">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>

      <div
        v-else-if="
          isValueSKU !== '' &&
          products.length === 0 &&
          productService.length === 0 &&
          isLoading === false
        "
      >
        <h6 class="not-exist">No article Exist</h6>
      </div>
      <div
        v-else-if="
          (isValueSKU !== '' && products.length > 0) ||
          (productService.length > 0 && isLoading === false)
        "
        class="search-sku"
      >
        <!-- <SearchResultSKU
                    :products="products"
                    :product-service="productService"
                    :list-item="listItem"
                    :disabler="disabledSKU"
                    @addProduct="addProduct"
                /> -->
      </div>
      <!-- <div v-if="productSelected !== null" class="product-detail">
                <ProductDetail :item="productSelected" />
            </div>
            <div v-if="productSelected !== null" class="related-promo">
                <RelatedPromo :items="eligiblePromotion" />
            </div> -->
    </div>

    <div class="grid-container-div2 relative">
      <div class="div1">
        <!-- <add-member
          :is-modal-active-more-option="isModalActiveMoreOption"
          :sales-type="listOrder.sales_type"
          :selected-member="selectedMember"
          :reset-customer="resetCustomer"
          :list-item="listItem"
          :is-loading="isLoading"
          :list-order-checked="listOrderChecked"
          :is-loading-return-exchange="isLoadingReturnExchange"
        /> -->
      </div>
      <div
        v-if="dataMember === null"
        class="div2 w-full"
        :class="
          listItem.length === 0 || listItem.every((item) => item.stock === '0')
            ? 'relative'
            : ''
        "
      >
        <div
          :class="
            listItem.length === 0 ||
            listItem.every((item) => item.stock === '0')
              ? 'no-item'
              : ''
          "
        ></div>
        <ListCheckout
          :list-item="listItem"
        />
      </div>
      <div
        v-if="dataMember === null"
        class="flying-bottom-container flex flex-col justify-around"
        :class="
          listItem.length === 0 || listItem.every((item) => item.stock === '0')
            ? 'relative'
            : ''
        "
      >
        <div
          :class="
            listItem.length === 0 ||
            listItem.every((item) => item.stock === '0')
              ? 'no-item'
              : ''
          "
        ></div>
      </div>
      <button class="btn-payment flex px-4 py-2">
        <span class="d-block text-white">Payment</span>
      </button>
    </div>
  </div>
</template>

<script>
import ListCheckout from '@/components/point-of-sales/ListCheckout'
export default {
  name: 'PointOfSaleage',
  components: {ListCheckout},
  data() {
    return {
      total: 0,
      discount: 0,
      isLoading: false,
      isLoadingReturnExchange: false,
      products: [],
      productService: [],
      productSelected: null,
      listItem: [{},{},{},{}],
      isSaveBillButton: false,
      isCouponButton: false,
      isCouponPromoButton: false,
      isVoucherLoyaltyButton: false,
      isAuthorizationModal: false,
      isRetailAssistantModal: false,
      isConfirmPayment: false,
      isAlertExistModal: false,
      dataMember: null,
      isSetAlert: false,
      listPaymentData: [],
      listOrderChecked: [],
      listItemExchange: [],
      listOrderReturnChecked: [],
      isValueSKU: '',
      salesType: 'Walk In',
      couponCode: '',
      voucherLoyaltyCode: '',
      isAlertModalMessage: '',
      skucodeSelected: [],
      checkAllOrder: false,
      isDeleteItem: false,
      invoiceNumberReturnTemp: '',
      listOrderReturn: {},
      selectedMember: null,
      invoice_number: '',
      activeModal: '',
      listOrder: false,
      resetCustomer: false,
      isLoyaltyButton: false,
      loyaltyPointPayload: {},
      couponPromoCode: {},
      eligiblePromotion: [],
      paymentDisabler: [],
      isRequired: '',
      isModalActiveMoreOption: false,
      disabledSKU: false,
    }
  },
}
</script>

<style lang="css" scoped>
.alert {
  width: 100% !important;
  text-align: center;
}
.translateAlert {
  opacity: 0;
  transition: 0.5s ease-in;
  visibility: hidden;
}
.activeAlert {
  opacity: 1;
  transition: 0.5s ease-in;
  visibility: inherit;
}
.collapsible-group {
  border: 1px solid rgba(221, 221, 221, 0.7);
}
.payment-type {
  border-bottom: 1px solid rgba(221, 221, 221, 0.7);
  font-family: 'Druk Text';
}
.no-item {
  position: absolute;
  height: 100%;
  width: 100%;
  background-color: rgba(247, 247, 247, 0.5);
}
.not-exist {
  color: #929292;
}
.total-qty {
  font-size: 16px;
}
.payment-button {
  background-color: #fd4513;
  border: none;
  padding: 0.8em 1em;
  border-radius: 7px;
  font-size: 1.1em;
  font-weight: bold;
  color: #fff;
  letter-spacing: 0.1em;
}
.payment-button:hover {
  cursor: pointer;
  background-color: #ff3700;
}

.grid-container-div1 {
  height: calc(100vh - 97px);
  flex: 0 40%;
  display: flex;
  align-items: center;
  flex-direction: column;
  background-color: rgba(221, 221, 221, 0.3);
  overflow-y: scroll;
  padding: 1em;
}
.search-sku,
.related-promo,
.product-detail {
  width: 100%;
}
.grid-container-div1 > * {
  margin-bottom: 0.8em;
}
.grid-container {
  min-height: calc(100vh - 97px);
  display: flex;
  position: relative;
}
.grid-container-div2 {
  flex: 0 60%;
  border-left: 2px solid rgba(221, 221, 221, 0.7);
}
.grid-container-div2 .div2 {
  overflow-y: scroll;
  height: calc(90vh - 97px);
}

.grid-container-div2 .div2::-webkit-scrollbar {
  width: 0.3em;
  border-radius: 18px;
}
.grid-container-div2 .div2::-webkit-scrollbar-track {
  opacity: 0.32;
  border-radius: 18px;
  background-color: rgba(238, 238, 238, 0.438);
}

.grid-container-div2 .div2::-webkit-scrollbar-thumb {
  background-color: #b3b7c6;

  border-radius: 18px;
}
.grid-container-div2 .div3 {
  grid-area: 12 / 1 / 15 / 2;
}
.grid-container-div2 .div3 .btn--ghost-orange {
  padding: 0.5em 0;
  margin: 0 0.5em;
  width: 33.3%;
  border-radius: 7px;
  font-weight: 600;
}
.flying-bottom-container {
  width: 100%;
  background: #fff;
}

.container-btn {
}
.container-btn > * {
}
.container-btn:first-child {
  flex: 0 20%;
  width: 20%;
}

.container-btn:last-child {
  flex: 0 80%;
  width: 80%;
}

.btn-payment {
  background: #fd4513;
}
</style>
