<script setup>

</script>

<template>
  <section class="page_404">
        <div class="w-3/5 mx-auto">
          <div class="text-center">
            <div class="four_zero_four_bg">
              <h1 class="text-center ">404</h1>
            </div>

            <div class="contant_box_404">
              <h3 class="font-bold">
                Look like you're lost
              </h3>

              <p>the page you are looking for not avaible!</p>

              <router-link to="/" class="link_404">Go to Home</router-link>

            </div>
        </div>
    </div>
  </section>
</template>



<style scoped>
/*======================
    404 page
=======================*/

.page_404 {
  padding: 40px 0;
  background: #fff;
  font-family: 'Arvo', serif;
}

.page_404 img {
  width: 100%;
}

.four_zero_four_bg {

  background-image: url(https://cdn.dribbble.com/users/285475/screenshots/2083086/dribbble_1.gif);
  height: 400px;
  background-position: center;
}


.four_zero_four_bg h1 {
  font-size: 80px;
}

.four_zero_four_bg h3 {
  font-size: 100px;
  font-weight: bold;
}

.link_404 {
  color: #fff !important;
  padding: 10px 20px;
  background: #39ac31;
  margin: 20px 0;
  display: inline-block;
}

.contant_box_404 {
  margin-top: -50px;
}
</style>