<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
      <p class="subClaim">Begin your journey through our amazing galaxy,
        and discover places you never even heard of.</p>
      <p class="subClaim">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
  .claimWrapper{
    text-align:center;
    display: flex;
    flex-direction:column;
    justify-content: center;
    align-items: center;
    color: white;
    z-index: 2;
  }

  .claim{
    font-size: 50px;
    font-weight: 800;
    margin: 0;

    @media (min-width: 768px){
      font-size: 80px;
    }

   @media (min-width: 1024px) {
    font-size: 100px;
  }
  }

  .subClaim {
    margin: 20px 0 0 0;
    width: 90%;
    font-size: 13px;
    font-weight: 400;

    @media (min-width: 768px){
      font-size: 17px;
      line-height: 1;
      letter-spacing: 1px;
      width: 500px;
    }
  }

  h1{
    margin: 0;
    padding: 0;
  }
</style>
