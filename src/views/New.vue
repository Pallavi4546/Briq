<template>
  <div class="container">
    <strong style="font-size: 40px">Liked Quotes</strong>
    <div class="card m-5 p-5" v-for="(data, index) in item" :key="index">
      <div class="card-content">
        <strong style="font-size">"{{ data.text }}"</strong>
        <p>by '{{ data.author }}'</p>
      </div>
      <hr />
        <div
        class="icon m-2 p-1"
        style="color: gold; font-size: 30px"
        v-for="i in parseInt(data.rating)"
        :key="i"
      >
  <i class="fas fa-star"></i>
      </div>
      
    </div>
  </div>
</template>
<script>
export default {                        
  data() {
    return {
      item: null,
    };
  },
  created() {
    var allrating = JSON.parse(localStorage.getItem("ratedquote"));
    if (allrating) {
      this.item = allrating;
    }
  },
  
};
</script>
<style>
.card{
  width:80%;
  
}
.container{
  margin-left: 200px;
}
  </style>
