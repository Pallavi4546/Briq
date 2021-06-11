<template>
  <div class="container " style="margin-left:100px">
    <div class="card m-5 p-5" >
      <div class="card-content m-3 p-3">
        <strong style="font-size" v-if="user">"{{ user.text }}"</strong>
        <p v-if="user">by '{{ user.author }}'</p>
      </div>
      <br>
      <div class="columns">
          <div class="new column ">
            <input
              type="radio"
              id="star5"
              name="rate"
              value="5"
              v-model="rating"
            />
            <label for="star5">5 stars</label>
            <input
              type="radio"
              id="star4"
              name="rate"
              value="4"
              v-model="rating"
            />
            <label for="star4">4 stars</label>
            <input
              type="radio"
              id="star3"
              name="rate"
              value="3"
              v-model="rating"
            />
            <label for="star3">3 stars</label>
            <input
              type="radio"
              id="star2"
              name="rate"
              value="2"
              v-model="rating"
            />
            <label for="star2">2 stars</label>
            <input
              type="radio"
              id="star1"
              name="rate"
              value="1"
              v-model="rating"
            />
            <label for="star1">1 star</label>
            </div>
      <div class="column">
   <button class="button is-success m-5 p-2" @click="storedata(user, rating)" style="float:left">
      submit
    </button>
     <div class="column">
   <button class="button is-info m-5 p-2"  style="float:left">
      <i class="fas fa-redo-alt" type="button" @click="reload()"></i>
    </button>
      </div>
      </div>
      </div>
    </div>
    <!-- {{ item }} -->
    
    <!-- {{ rating }} -->
    <!-- {{ ratedquote }} -->
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      user: null,
      rating: null,
      ratedquote: [],
      item: [],
    };
  },
  created() {
    axios.get("https://type.fit/api/quotes").then((res) => {
      this.user = res.data[Math.floor(Math.random() * res.data.length)];
    });
    var allrating = JSON.parse(localStorage.getItem("ratedquote"));
    if (allrating) {
      this.item = allrating;
    }
  },
  methods: {
    storedata(user, rating) {
      if (rating == "4" || rating == "5") {
        this.ratedquote.push({ ...user, rating: rating });
        this.ratedquote.forEach((element) => {
          this.item.push({ ...element });
          // console.log("ele", { ...element });
          // console.log("fwe", this.item);
        });
        localStorage.setItem("ratedquote", JSON.stringify(this.item));
      }
      alert("Thank you for rating the Quote")
      console.log("new", this.ratedquote);
    },
    reload(){
      window.location.reload()
    }
  },
};
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
}

.new:not(:checked) > input {
  position: relative;
  top: -9999px;        
}
.new:not(:checked) > label {
  float: right;  
  width: 42px;
  overflow: hidden;
  white-space: nowrap;  
  cursor: pointer;
  font-size: 30px;
  color: #ccc;
}
.new:not(:checked) > label:before {
  content: 	'\2605';
  font-size: 50px;
}
.new > input:checked ~ label {
  color: gold;
}
/* .new:not(:checked) > label:hover, */
.new:not(:checked) > label:hover ~ label {
  color: #deb217;
}

/* .new > input:checked ~ label:hover, */
.new > label:hover ~ input:checked ~ label {
  color: #c59b08;
}

</style>