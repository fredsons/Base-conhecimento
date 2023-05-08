<template>
    <footer class="footer">
        <span> <img class="rodape" src="@/assets/logo.png" alt=""> <strong> 2023 Entreposto.</strong> <strong> Todos os direitos reservados. </strong> </span> 
    </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style>
.footer {
  grid-area: footer;
  background-color: #ddd;
  color: #333;

  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 10px;
}

.rodape {
  width: 30px;
  margin-right: 5px;
}
</style>
