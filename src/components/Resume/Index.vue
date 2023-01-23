<template>
    <main> 
        <p>{{labelVisual}}</p>
        <h1>{{amountCurrency}}</h1>
        <div class="graphic">
          <slot name="graphic"></slot>
        </div>
        <div class="action">
          <slot name="action"></slot>
        </div>
    </main>
</template>

<script setup>
import {defineProps, computed, toRefs} from "vue";

const currencyFormatter = new Intl.NumberFormat("pt-BR", {
 style: "currency",
 currency: "BRL",
 })

const props = defineProps({
        totalLabel: String,
        label: String,
        totalAmount: Number,
        amount: Number
    });

const {amount, totalAmount, totalLabel, label} = toRefs(props);

const amountVisual = computed(() => {
    return amount.value !== null ? amount.value : totalAmount.value
  
});

const labelVisual = computed(() =>{
  return label.value !== null ? label.value : totalLabel.value

});

const amountCurrency = computed(() =>{
  return currencyFormatter.format(amountVisual.value)

});


</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>