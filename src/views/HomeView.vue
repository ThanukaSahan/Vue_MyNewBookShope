<template>
  <div>
    <div class="center-text">
      <p>This page is under Development.</p>
      <p>
        Please click<router-link to="/BookshopeSale" class="nav-link"
          >Books</router-link
        >
        to purchase books.
      </p>
      <img src="../assets/BgCons.jpg" />
    </div>
  </div>
</template>

<script>
export default {};
</script>
<style scoped>
.center-text {
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  color: #1242c7; /* Blue color, you can change this */
  margin-top: 5%;
}
a {
  text-decoration: dotted;
  color: blueviolet;
  text-transform: capitalize;
}

img{
  width: 400px;
  height: auto;
}
</style>
