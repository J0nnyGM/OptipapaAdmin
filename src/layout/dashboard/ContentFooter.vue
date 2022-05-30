<template>
  <footer class="footer">
    <div class="container-fluid">
      <ul class="nav">
       
      </ul>
      <div class="copyright">
        © {{year}}  <i class="tim-icons icon-heart-2"></i> 
        <a href="https://www.binarcode.com" target="_blank" rel="noopener"></a>&nbsp;&
        <a href="https://www.creative-tim.com" target="_blank" rel="noopener">OptiPapa</a> .
      </div>
    </div>
  </footer>
</template>
<script>
  export default {
    data() {
      return {
        year: new Date().getFullYear()
      }
    }
  };
</script>
<style>
</style>
