<template>
  <section class="carousel-wrapper">
    <button
      type="button"
      class="arrows left-arrow arrow-inactive"
      aria-label="Arrow Left"
    >
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 512">
        <!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
        <path
          d="M192 448c-8.188 0-16.38-3.125-22.62-9.375l-160-160c-12.5-12.5-12.5-32.75 0-45.25l160-160c12.5-12.5 32.75-12.5 45.25 0s12.5 32.75 0 45.25L77.25 256l137.4 137.4c12.5 12.5 12.5 32.75 0 45.25C208.4 444.9 200.2 448 192 448z"
        />
      </svg>
    </button>
    <section class="carousel">
      <div class="carousel-item">
        <RouterLink :to="{ name: 'testView' }">
          <div
            style="
              background-image: url(../../assets/test.jpg);
              width: 200px;
              height: 300px;
            "
          >
            <div style="padding-top: 100%">
              <p style="font-size: 20px; margin-top: 10%">실험실</p>
              <p>여러가지를 테스트해보세요!</p>
            </div>
          </div></RouterLink
        >
      </div>
      <div class="carousel-item">
        <RouterLink :to="{ name: 'ArticleView' }"
          ><div
            style="
              background-image: url(../../assets/community.jpg);
              width: 200px;
              height: 300px;
            "
          >
            <div style="padding-top: 100%">
              <p style="font-size: 20px; margin-top: 10%">커뮤니티</p>
              <p>은행, 금융상품, 일상 얘기</p>
            </div>
          </div></RouterLink
        >
      </div>
      <div class="carousel-item">
        <RouterLink :to="{ name: 'ExchangerView' }">
          <div
            style="
              background-image: url(../../assets/yellow_background.jpg);
              width: 200px;
              height: 300px;
            "
          >
            <div style="padding-top: 100%">
              <p style="font-size: 20px; margin-top: 10%">환율계산기</p>
              <p>원을 달러로</p>
            </div>
          </div></RouterLink
        >
      </div>
      <div class="carousel-item">
        <RouterLink :to="{ name: 'BankView' }">
          <div
            style="
              background-image: url(../../assets/product.jpg);
              width: 200px;
              height: 300px;
            "
          >
            <div style="padding-top: 100%">
              <p style="font-size: 20px; margin-top: 10%">영업점 찾기</p>
              <p>우리집에서 가장 가까운 은행</p>
            </div>
          </div></RouterLink
        >
      </div>
      <div class="carousel-item">
        <RouterLink :to="{ name: 'DepositGeneralRecommendationView' }">
          <div
            style="
              background-image: url(../../assets/Bee.jpg);
              width: 200px;
              height: 300px;
            "
          >
            <div style="padding-top: 100%">
              <p style="font-size: 20px; margin-top: 10%">금융상품 추천</p>
              <p>예금 적금 추천받아요</p>
            </div>
          </div></RouterLink
        >
      </div>
    </section>
    <button type="button" class="arrows right-arrow" aria-label="Arrow Right">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 512">
        <!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
        <path
          d="M64 448c-8.188 0-16.38-3.125-22.62-9.375c-12.5-12.5-12.5-32.75 0-45.25L178.8 256L41.38 118.6c-12.5-12.5-12.5-32.75 0-45.25s32.75-12.5 45.25 0l160 160c12.5 12.5 12.5 32.75 0 45.25l-160 160C80.38 444.9 72.19 448 64 448z"
        />
      </svg>
    </button>
  </section>
  <v-container style="padding-right: 30%; padding-left: 30%"
    ><section id="toggle-overflow">
      <h2>스크롤바 표시</h2>
      <input id="toggle" type="checkbox" />
      <label for="toggle">
        <p id="on">ON</p>
        <p id="off">OFF</p>
      </label>
    </section></v-container
  >
</template>

<script setup>
import { onMounted } from "vue";
import { useCounterStore } from "@/stores/product";

const store = useCounterStore();

onMounted(() => {
  store.saveProducts();
  store.saveOptions();
});

function scrollEv(leftArrow, rightArrow, carousel) {
  if (carousel.scrollLeft <= 0) {
    leftArrow.classList.add("arrow-inactive");
  } else {
    leftArrow.classList.remove("arrow-inactive");
  }
  if (carousel.scrollLeft >= carousel.scrollWidth - carousel.offsetWidth - 1) {
    rightArrow.classList.add("arrow-inactive");
  } else {
    rightArrow.classList.remove("arrow-inactive");
  }
}

function clicleftArrow(carousel, rectList) {
  let shiftScroll;
  for (let i = 0; i < rectList.length; i++) {
    if (carousel.scrollLeft > rectList[rectList.length - 1]) {
      shiftScroll = rectList[rectList.length - 1];
    } else if (
      carousel.scrollLeft > rectList[i] &&
      carousel.scrollLeft <= rectList[i + 1]
    ) {
      shiftScroll = rectList[i];
    }
  }
  carousel.scrollTo({
    left: shiftScroll,
    behavior: "smooth",
  });
}

function clickRight(carousel, rectList) {
  let shiftScroll;
  for (let i = 0; i < rectList.length; i++) {
    if (
      carousel.scrollLeft >= rectList[i] - 1 &&
      carousel.scrollLeft < rectList[i + 1]
    ) {
      shiftScroll = rectList[i + 1];
    }
  }
  carousel.scrollTo({
    left: shiftScroll,
    behavior: "smooth",
  });
}

function listRectCarousel(carouselNumber, carousels) {
  let divs = carousels[carouselNumber].getElementsByClassName("carousel-item");
  let rectList = [];
  let rectGauche = carousels[carouselNumber].getBoundingClientRect().left;

  for (let i = 0; i < divs.length; i++) {
    let rect = divs[i].getBoundingClientRect();
    rectList.push(rect.left - rectGauche);
  }

  for (let i = rectList.length - 1; i >= 0; i--) {
    rectList[i] = rectList[i] - rectList[0];
  }
  return rectList;
}

function autoSlidePosLeft(carouselNumber, carousels, leftArrows) {
  let rectList = listRectCarousel(carouselNumber, carousels);
  leftArrows[carouselNumber].addEventListener("click", () => {
    clicleftArrow(carousels[carouselNumber], rectList);
  });
}

function autoSlidePosRight(carouselNumber, carousels, rightArrows) {
  let rectList = listRectCarousel(carouselNumber, carousels);
  rightArrows[carouselNumber].addEventListener("click", () => {
    clickRight(carousels[carouselNumber], rectList);
  });
}

window.onload = () => {
  let leftArrows = document.getElementsByClassName("left-arrow");
  let rightArrows = document.getElementsByClassName("right-arrow");
  let carousels = document.getElementsByClassName("carousel");

  for (let i = 0; i < leftArrows.length; i++) {
    autoSlidePosLeft(i, carousels, leftArrows);
    window.onresize = () => {
      autoSlidePosLeft(i, carousels, leftArrows);
    };
  }

  for (let i = 0; i < rightArrows.length; i++) {
    autoSlidePosRight(i, carousels, rightArrows);
    window.onresize = () => {
      autoSlidePosRight(i, carousels, rightArrows);
    };
  }

  for (let i = 0; i < carousels.length; i++) {
    carousels[i].addEventListener("scroll", () => {
      scrollEv(leftArrows[i], rightArrows[i], carousels[i]);
    });
  }

  for (let i = 0; i < carousels.length; i++) {
    scrollEv(leftArrows[i], rightArrows[i], carousels[i]);
    window.onresize = () => {
      scrollEv(leftArrows[i], rightArrows[i], carousels[i]);
    };
  }

  /* TOGGLE OVERFLOW */

  let toggleOverflow = document.getElementById("toggle");
  toggleOverflow.addEventListener("click", () => {
    for (let i = 0; i < carousels.length; i++) {
      carousels[i].classList.toggle("overflow");
      carousels[i].parentNode.classList.toggle("scrollbar-overflow");
    }
  });
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: #dbd5d1;
  font-family: "Roboto", sans-serif;
  gap: 1em;
}

.carousel-wrapper {
  display: flex;
  justify-content: space-between;
  gap: 0.5em;
  max-width: 1000px;
  width: 90%;
  margin-top: 10%;
  margin-left: auto;
  margin-right: auto;
}

.wrapped-container {
  display: flex;
  overflow: hidden;
  width: 95%;
  justify-content: center;
}

.carousel {
  width: 100%;
  height: 100%;
  position: relative;
  overflow-y: hidden;
  display: flex;
  gap: 1em;
  scrollbar-width: none;
}

.arrows {
  width: 20px;
  height: 45px;
  outline: none;
  border: none;
  background-color: #5e4c5a;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  align-self: center;
  opacity: 1;
  cursor: pointer;
  transition: all 0.1s ease;
  padding: 0;
  pointer-events: all;
}

.arrows:hover {
  background-color: #5e4c5a;
  transform: scale(1.1);
}

.arrows svg {
  width: 1.5em;
  height: 1.5em;
  fill: white;
}

.arrow-inactive {
  opacity: 0.5;
  cursor: auto;
}

.arrow-inactive:hover {
  transform: none;
}

.carousel-item {
  width: 200px;
  height: 300px;
}

.carousel-item div {
  border-radius: 10pt;
}

input[type="checkbox"] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label {
  color: white;
  cursor: pointer;
  width: 50px;
  height: 30px;
  background: #5e4c5a;
  display: block;
  border-radius: 100px;
  position: relative;
}

label:after {
  content: "";
  position: absolute;
  top: 5px;
  left: 5px;
  width: 20px;
  height: 20px;
  background: #fff;
  border-radius: 90px;
  transition: 0.3s;
}

input:checked + label {
  background: #ef8354;
}

input:checked + label:after {
  left: calc(100% - 5px);
  transform: translateX(-100%);
}

label:active:after {
  width: 20px;
}

input:checked + label #off {
  display: none;
}

:not(input:checked) + label #on {
  display: none;
}

p {
  margin: 0;
  padding: 0;
  height: 100%;
  display: flex;
  align-items: center;
  font-size: 0.75rem;
  user-select: none;
  padding-left: 0.5em;
  padding-right: 0.35em;
  font-weight: 600;
}

#off {
  justify-content: flex-end;
  font-size: 0.65rem;
}

#toggle-overflow {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  gap: 0.25em;
  color: #5e4c5a;
  font-size: 0.75rem;
}

.overflow {
  overflow-x: auto;
  scrollbar-width: thin;
}

.carousel-wrapper.scrollbar-overflow ::-webkit-scrollbar {
  height: 6px;
}

.carousel-wrapper ::-webkit-scrollbar {
  height: 0px;
}

.carousel-wrapper ::-webkit-scrollbar-track {
  background: #c0b6af;
  border-radius: 10pt;
}

.carousel-wrapper ::-webkit-scrollbar-thumb {
  background: #5e4c5a;
  border-radius: 10pt;
}

.carousel-wrapper ::-webkit-scrollbar-thumb:hover {
  background: #2d242b;
}

@media (pointer: coarse) {
  .carousel {
    overflow-x: auto;
    scrollbar-width: thin;
  }
  .carousel-wrapper ::-webkit-scrollbar {
    height: 6px;
  }
}
</style>
