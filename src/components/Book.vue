<template>
  <div id="book-wrapper">
    <div class="container">
      <div class="row overflownone">
        <div class="col-md-4 information nopaddingleft nopaddingright hidden-sm hidden-xs">
          <h3>Vintri Test</h3>
          <ul class="information_menu">
            <li 
              @mouseover="hItem = 1" 
              @mouseleave="hItem = 0"
              :class="[{'active': hItem == 1}]"
              >
              Overview 
            </li>
            <li 
              @mouseover="hItem = 2"
              @mouseleave="hItem = 0"
              :class="[{'active': hItem == 2}]"
              >
              Book Details
            </li>
            <li 
              @mouseover="hItem = 3"
              @mouseleave="hItem = 0"
              :class="[{'active': hItem == 3}]"
              >
              Library Details
            </li>
            <li 
              @mouseover="hItem = 4"
              @mouseleave="hItem = 0"
              :class="[{'active': hItem == 4}]"
              >
              Collection Details
            </li>
            <li 
              @mouseover="hItem = 5"
              @mouseleave="hItem = 0"
              :class="[{'active': hItem == 5}]"
              >
              Loan History
            </li>
          </ul>
        </div>
        <div class="col-md-8 nopaddingleft nopaddingright">
          <div class="slideshow">
            <div class="overlay-id1 overlay-item" :class="[{'active': hItem == 1}]">
              <h3>Overview</h3>
              <ul class="quickmenu">
                <li><a href="#" title="#">Title: {{book.title}}</a></li>
                <li><a href="#" title="#">Overview: {{book.overview}}</a></li>
                <li><a href="#" title="#">Author(s): <span v-for="(a, i) in book.authors" :key="i">{{a}}</span></a></li>
                <li><a href="#" title="#">Edition: {{book.edition}}</a></li>
                <li><a href="#" title="#">Published Date: {{book.date_published}}</a></li>
              </ul>
            </div>
            <div class="overlay-id2 overlay-item" :class="[{'active': hItem == 2}]">
              <h3>Book Details</h3>
              <ul class="quickmenu">
                <li><a href="#" title="#">Tags: <span v-for="(t, ti) in book.tags" :key="ti">{{`${t}, `}}</span></a></li>
                <li><a href="#" title="#">Weight: <span v-for="(w, wi) in book.weight" :key="wi">{{`${w}, `}}</span></a></li>
                <li><a href="#" title="#">Org Price: {{book.original_price}}</a></li>
                <li><a href="#" title="#">Website: {{book.website}}</span></a></li>
                <li><a href="#" title="#">Subjects: <span v-for="(s, si) in book.subjects" :key="si">{{`${s}, `}}</span></a></li>
              </ul>
            </div>
            <div class="overlay-id3 overlay-item" :class="[{'active': hItem == 3}]">
              <h3>Library Details</h3>
              <ul class="quickmenu">
                <li><a href="#" title="#">Branch: {{book.current_branch}}</a></li>
                <li><a href="#" title="#">Status: {{book.current_status}}</a></li>
                <li><a href="#" title="#">Hold Count: {{book.hold_count}}</a></li>
                <li><a href="#" title="#">Number of copies: {{book.number_of_copies}}</a></li>
                <li><a href="#" title="#">Due Date: {{book.due_date}}</a></li>
              </ul>
            </div>
            <div class="overlay-id4 overlay-item" :class="[{'active': hItem == 4}]">
              <h3>Collection Details</h3>
              <ul class="quickmenu">
                <li v-for="(c, ci) in book.collection" :key="ci"><a href="#" title="#">{{c}}</a></li>
              </ul>
            </div>
            <div class="overlay-id5 overlay-item" :class="[{'active': hItem == 5}]">
              <h3>Loan History</h3>
              <ul class="quickmenu">
                <li v-for="(l, li) in book.loan_history" :key="li">
                  <a v-if="l.check_out" href="#" title="#">
                    OUT <br/>
                    By: {{l.check_out.check_out_by}}<br/>
                    Location: {{l.check_out.check_out_location}}<br/>
                    Date: {{l.check_out.check_out_date}}<br/>
                    Condition: {{l.check_out.check_out_condition}}<br/>
                  </a>
                  <a v-if="l.check_in" href="#" title="#">
                    IN <br/>
                    Librarian_id: {{l.check_in.check_in_librarian_id}}<br/>
                    Location: {{l.check_in.check_in_location}}<br/>
                    Date: {{l.check_in.check_in_date}}<br/>
                    Condition: {{l.check_in.check_in_condition}}<br/>
                  </a>
                </li>
              </ul>
            </div>
            <div id="carousel-example-generic" class="carousel slide carousel-fade" data-ride="carousel" ref="carousel">
              <!-- Wrapper for slides -->
              <div class="carousel-inner" role="listbox">
                <div class="item active">
                  <div class="carousel-caption">
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import BookJson from '../assets/book.json'

Vue.use(VueAxios, axios);

export default {
  data () {
    return {
      book: BookJson,
      hItem: Number,
    }
  },
  mounted(){
    this.hItem = 1
    this.fetchData()
  },
  methods:{
    fetchData(){
      axios.get(`${this.baseUrl}book.json`).then((response) => {
        if (response.data.length === 0) { 
          console.log('No items found')
          return
        } else { 
          console.log(response.data)
        }
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>

<style>
  html {
    font-size: 75%;
  }

  body {
    font-size: 14px;
    font-size: 14px;
    font-size: 1.4rem;
    background: #f5f5f5;
  }

  h3 {
    font-size: 24px;
    font-size: 24px;
    font-size: 2.4rem;
  }

  .nopaddingleft {
    padding-left: 0;
  }

  .nopaddingright {
    padding-right: 0;
  }

  .overflownone {
    overflow: hidden!important;
  }

  .information {
    background: #2a3d46;
    position: relative;
    height: 100vh;
  }

  .information h3 {
    font-size: 34px;
    font-size: 3.4rem;
    font-family: "roboto", sans-serif;
    font-weight: 500;
    color: #FFF;
    padding: 0 15px;
    margin: 20px 0;
  }

  .information .information_menu {
    padding: 0;
  }

  .information .information_menu li {
    list-style: none;
    position: relative;
    color: white;
    padding: 15px;
    cursor: pointer;
  }

  .information .information_menu li.active {
    background: #0383c5;
  }

  .information .information_menu li.active:after {
    content: "";
    width: 0;
    height: 0;
    border-top: 27px solid transparent;
    border-bottom: 27px solid transparent;
    border-left: 22px solid #0383c5;
    position: absolute;
    right: -22px;
    z-index: 1000;
    top: 0;
  }

  .information .information_menu li a {
    color: #FFF;
    display: block;
    padding: 16px 20px;
    font-size: 15px;
    font-size: 1.5rem;
    text-decoration: none;
  }

  .information .btn-emergency {
    background: #f89406;
    border: none;
    margin: 20px;
    display: block;
    width: 88%;
    color: #fff;
    text-shadow: none;
    padding: 0;
    font-size: 20px;
    font-size: 2rem;
  }

  .information .btn-emergency span {
    padding: 15px;
    display: block;
    background-size: 30px 30px;
    background-image: -webkit-gradient(linear, left top, right bottom, color-stop(0.25, rgba(255, 255, 255, .15)), color-stop(0.25, transparent), color-stop(0.5, transparent), color-stop(0.5, rgba(255, 255, 255, .15)), color-stop(0.75, rgba(255, 255, 255, .15)), color-stop(0.75, transparent), to(transparent));
    background-image: -webkit-linear-gradient(135deg, rgba(255, 255, 255, .15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, .15) 50%, rgba(255, 255, 255, .15) 75%, transparent 75%, transparent);
    background-image: -o-linear-gradient(135deg, rgba(255, 255, 255, .15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, .15) 50%, rgba(255, 255, 255, .15) 75%, transparent 75%, transparent);
    background-image: linear, 135deg, rgba(255, 255, 255, .15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, .15) 50%, rgba(255, 255, 255, .15) 75%, transparent 75%, transparent;
    -webkit-animation: animate-stripes 3s linear infinite;
    -moz-animation: animate-stripes 3s linear infinite;
  }

  .mobile-menu-bg {
    background: #2a3d46;
  }

  .information_menu_mobile {
    margin: 0px;
    padding: 0;
  }

  .information_menu_mobile li {
    padding: 0;
    float: left;
    width: 25%;
    list-style: none;
    text-align: center;
  }

  .information_menu_mobile li a {
    display: block;
    padding: 10px;
    color: #FFF;
    text-decaration: none;
  }

  .information_menu_mobile li:hover a {
    background: #0383c5;
    text-decaration: none;
  }

  .slideshow {
    overflow: hidden;
  }

  .slideshow .overlay-item {
    position: absolute;
    top: 0;
    z-index: 999;
    width: 720px;
    background: rgba(248, 148, 6, 0.67);
    height: 100vh;
    padding: 10px 30px;
    display: none;
    -webkit-animation: opendoor 0.75s ease 0s alternate;
    -webkit-transform-style: preserve-3d;
    transform-style: preserve-3d;
  }

  .slideshow .overlay-item.active {
    display: block;
    -webkit-animation: opendoor 0.75s ease 0s alternate;
    -webkit-transform-style: preserve-3d;
    transform-style: preserve-3d;
  }

  .slideshow .overlay-item.inactive {
    display: block;
    -webkit-animation: closedoor 0.75s ease 0s alternate;
    transform-style: preserve-3d;
    opacity: 0;
  }

  .slideshow .overlay-item .quickmenu {
    padding: 0;
  }

  .slideshow .overlay-item .quickmenu li {
    list-style: none;
  }

  .slideshow .overlay-item .quickmenu li a {
    color: #FFF;
    display: block;
    padding: 8px 20px;
    font-size: 15px;
    font-size: 1.5rem;
    text-decoration: none;
  }

  #slider {
    padding: 0px;
    margin: 0px
  }

  #slider li {
    padding: 0px;
    list-style: none;
    position: absolute;
  }

  #carousel-example-generic {
    height: 100vh;
  }

  .carousel-fade .carousel-inner .item {
    -webkit-transition-property: opacity;
    transition-property: opacity;
  }

  .carousel-fade .carousel-inner .item,
  .carousel-fade .carousel-inner .active.left,
  .carousel-fade .carousel-inner .active.right {
    opacity: 0;
    filter: alpha(opacity=0);
  }

  .carousel-fade .carousel-inner .active,
  .carousel-fade .carousel-inner .next.left,
  .carousel-fade .carousel-inner .prev.right {
    opacity: 1;
    filter: alpha(opacity=100);
  }

  .carousel-fade .carousel-inner .next,
  .carousel-fade .carousel-inner .prev,
  .carousel-fade .carousel-inner .active.left,
  .carousel-fade .carousel-inner .active.right {
    left: 0;
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  .carousel-fade .carousel-control {
    z-index: 2;
  }

  html,
  body,
  .carousel,
  .carousel-inner,
  .carousel-inner .item {
    height: 100%;
  }

  .item:nth-child(1) {
    background: #74C390;
  }

  .item:nth-child(2) {
    background: #51BCE8;
  }

  .item:nth-child(3) {
    background: #E46653;
  }

  @-webkit-keyframes animate-stripes {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 60px 0;
    }
  }

  @-webkit-keyframes in {
    from {
      -webkit-transform: scale(1.3);
    }
    to {
      -webkit-transform: scale(1);
    }
  }

  @-webkit-keyframes out {
    0% {
      -webkit-transform: scale(1);
    }
    100% {
      -webkit-transform: scale(1.3);
    }
  }

  @-webkit-keyframes opendoor {
    from {
      -webkit-transform: perspective(1000px) rotateY(90deg);
      -webkit-transform-origin: 0% 50%;
    }
    to {
      -webkit-transform: perspective(1000px) rotateY(0deg);
      -webkit-transform-origin: 0% 50%;
    }
  }

  @-webkit-keyframes closedoor {
    from {
      opacity: 1;
      -webkit-transform-origin: 0% 50%;
    }
    to {
      opacity: 0;
      -webkit-transform-origin: 0% 50%;
    }
  }
</style>
