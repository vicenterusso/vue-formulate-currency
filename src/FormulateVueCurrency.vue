<template>
   <currency-input
      type="text"
      v-model="context.model"
      v-bind="context.attributes"
      @blur="context.blurHandler"
      :currency=currency
      :locale=locale
      :precision=precision
      :auto-decimal-mode=autoDecimalMode
      :distraction-free=distractionFree
      :hide-currency-symbol=hideCurrencySymbol
  />
</template>

<script>
import { parse } from "vue-currency-input";
import VueCurrencyInput from 'vue-currency-input'

export default {
  components: {
    'currency': VueCurrencyInput,
  },
  props: {
    context: {
      type: Object,
      required: true
    },
  },
  computed: {
    currencyConfig() {
        return this.context.attributes.config;
    },
    myType() {      
        if(typeof this.context.attributes.subtype !== 'undefined' &&
            this.context.attributes.subtype === 'porcentagem')
            return 'percent';
        return 'money'
    },
    currency() {    
        return this.myType === 'money' ? this.currencyConfig.money().currency : this.currencyConfig.porcentagem().currency;
    },
    locale() {    
        return this.myType === 'money' ? this.currencyConfig.money().locale : this.currencyConfig.porcentagem().locale;
    },
    precision() {    
        return this.myType === 'money' ? this.currencyConfig.porcentagem().precision : this.currencyConfig.porcentagem().precision;
    },
    autoDecimalMode() {    
        return this.myType === 'money' ? this.currencyConfig.porcentagem().autoDecimalMode : this.currencyConfig.porcentagem().autoDecimalMode;
    },
    distractionFree() {    
        return this.myType === 'money' ? this.currencyConfig.porcentagem().distractionFree : this.currencyConfig.porcentagem().distractionFree;
    },
    hideCurrencySymbol() {    
        return this.myType === 'money' ? this.currencyConfig.porcentagem().hideCurrencySymbol : this.currencyConfig.porcentagem().hideCurrencySymbol;
    },
  },
}
</script>