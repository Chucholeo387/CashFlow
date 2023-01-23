<template>
    <header>
        <img
        @click="reload"
        src="https://static.platzi.com/media/public/uploads/cashflow-icon_73798840-dd9d-4253-9c6d-821fe57c686a.svg" 
        alt="Logo">
        <h1><span>Cash</span>Flow</h1>
    </header>
</template>

<script setup>

    function reload(){
        location.reload()
    }
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100vw;
}
img,
span {
  width: 48px;
}
h1 {
  font-size: 1.4rem;
  color: var(--brand-blue);
}
h1 span {
  color: var(--brand-green);
}
</style>