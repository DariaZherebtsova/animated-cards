<template>
  <div class="cards">
    <div class="card card--first">
      <div class="card__front"></div>
      <div class="card__back"></div>
    </div>
    <div class="card card--second"></div>
    <div class="card card--third"></div>
    <div 
      class="card card--fourth"
      :class="{ 'active': active }"
      @click="startAnimation"
    >
      <div class="card__text">
        click
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const active = ref(false);

const startAnimation = () => {
  active.value = true;
  setTimeout(() => {
    active.value = false;
  }, 800);
}
</script>

<style lang="scss">
  .cards {
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 15px;
    width: 100%;
    @include tablet {
      grid-template-columns: repeat(2, 1fr);
      overflow: visible;
    }
    @include desktop {
      grid-template-columns: repeat(4, 1fr);
    }
  }
  .card {
    position: relative;
    min-width: 100px;
    width: 100%;
    height: 340px;
    border-radius: 22px;
    perspective: 1000px;
    @include tablet {
      height: 300px;
    }
    @include desktop {
      height: 340px;
    }

    path {
      stroke: #d8d8dd;
      stroke-width: 2px;
    }
    svg {
      position: absolute;
    }

    &__front, &__back {
      position: absolute;
      width: 100%;
      height: 100%;
      transition: 1s;
      backface-visibility: hidden;
      border-radius: 20px;
    }

    &__front {
      background-color: $primary;
    }
    &__back {
      background-color: $secondary;
      transform: rotateY(180deg);
    }

    &:hover {
      .card__front {
        transform: rotateY(180deg);
      }
      .card__back {
        transform: rotateY(360deg);
      }
    }

    &__text {
      color: $text-primary;
      opacity: 0;
      transition: opacity 1s;
      font-size: 16px;
    }
  }

  .card--second {
    background-color: $primary;
    transition: 1s;
    &:hover {
      z-index: 100;
      box-shadow: $primary-shadow 0px 5px 15px;
      transform: scale(1.2);
    }
  }

  .card--third {
    background-color: $primary;
    &:hover {
      box-shadow: $primary-shadow 0px 5px 15px;
      transform-origin: 50% 100%;
      animation: wiggle 3s linear infinite;
    }
  }

  .card--fourth {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: $primary;
    &:hover .card__text{
      opacity: 1;
    }
    &.active {
      background-color: rgb(116, 193, 168);
      transform-origin: 50% 100%;
      animation: swipe 800ms cubic-bezier(0.2, 0.8, 1, 2);
    }
  }


  @keyframes wiggle {
  0%, 7% {
    transform: rotateZ(0);
  }
  15% {
    transform: rotateZ(-15deg);
  }
  20% {
    transform: rotateZ(10deg);
  }
  25% {
    transform: rotateZ(-10deg);
  }
  30% {
    transform: rotateZ(6deg);
  }
  35% {
    transform: rotateZ(-4deg);
  }
  40%, 100% {
    transform: rotateZ(0);
  }
}

@keyframes swipe {
  0% {
    transform: rotate(0deg) translateX(15px);
  }
  100% {
    transform: rotate(16deg) translateX(450px);
  }
}
</style>
