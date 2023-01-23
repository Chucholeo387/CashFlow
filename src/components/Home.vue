
<template>
    <Layout>
        <template #header>
            <Header>
            </Header>
        </template>
        <template #resume>
            <Resume
                :total-label="'Ahorro total'"
                :label ="label"
                :total-amount ="totalAmount"
                :amount ="amount"
                
            >
            
                <template #graphic>
                    <Graphic :amounts="amounts" />
                </template>
                <template #action>
                    <Action @create="create" /> 
                </template>
            
            </Resume>
        </template>
        template
        <template #movements>
            <Movements
                :movements="movements"
                @remove="remove"
            
            />
        </template>
    </Layout>
</template>

<script setup>
import Layout from "./Layout.vue"
import Header from "./Header.vue"
import Resume from "./Resume/Index.vue"
import Movements from "./Movements/Index.vue"
import Action from "./Action.vue"
import Graphic from "./Resume/Graphic.vue"
import {computed, ref, } from "vue"

let amount = ref(null)
let label = ref(null)



let movements = ref([])


const amounts = computed(() =>{
  
 return movements.value.filter(m => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
         
          return m.time > oldDate;
         
        })
        .map(m => m.amount)
        .map((_, i, lastDays) => {
            const lastMovements = lastDays.slice(0, i + 1);
            return lastMovements.reduce((accAmount, amount) => accAmount + amount, 0);
        });
})

const totalAmount = computed(()=>{

    return movements.value.reduce((suma, m) =>{
        return suma + m.amount
    }, 0)

})

 
const create = (movement) => {
  movements.value.push(movement)
  save()
}

 const remove = (id) => {
      const index = movements.value.findIndex(m => m.id === id);
      movements.value.splice(index, 1);
      save()
    }

  const save = ()=> {
    localStorage.setItem("movements", movements.value)
  }
</script>

