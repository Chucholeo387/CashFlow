<template>
    <div class="movement">
        <div class="content">
            <h4>{{title}}</h4>
            <p>{{description}}</p>
        </div>
        <div class="action">
            <img src="https://static.platzi.com/media/public/uploads/trash-icon_5de37388-586f-4cb9-8ba9-1fabd994cb28.svg" alt="icono de basura" @click="remove">
            <p :class="{'red': isNegative , 'green': !isNegative }">{{amountCurrency}}</p>
        </div>
    </div>
</template>

<script setup>
import { toRefs, defineProps, computed, defineEmits } from 'vue';

const props = defineProps({
    id: {
        type: Number,
    },
    title: {
        type: String,
    },
    description: {
        type: String,
    },
    amount: {
        type: Number,
    }
});
const { title, id, description, amount } = toRefs(props);


const currencyFormatter = new Intl.NumberFormat("pt-BR", {
 style: "currency",
 currency: "BRL",
 });

const amountCurrency = computed(()=> currencyFormatter.format(amount.value) );

const isNegative = computed(()=>  amount.value < 0 )



const emit = defineEmits(["remove"])

const remove = () => {
    emit("remove", id.value)

}



</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
    color: red;
}
.green {
    color: green;
}
</style>