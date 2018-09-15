<template>
  <div class="sunset">
    <div class="background-line background-line--sky"></div>
    <div class="background-line background-line--sky"></div>

    <div class="background-line background-line--sky background-line--has-clouds">
      <span class="cloud cloud--double cloud--reverse cloud--1"></span>
      <span class="cloud cloud--2"></span>
    </div>

    <div class="background-line background-line--sky"></div>

    <div class="background-line background-line--sky"></div>

    <div class="background-line background-line--sky
                background-line--contains-sun
                background-line--has-clouds">
      <span class="cloud cloud--double cloud--3"></span>
      <span class="cloud cloud--double cloud--4"></span>
      <div class="sun"></div>
      <span class="cloud cloud--5"></span>
    </div>

    <div class="background-line background-line--sea"></div>
    <div class="background-line background-line--sea"></div>
    <div class="background-line background-line--sea"></div>
    <div class="background-line background-line--sea"></div>
  </div>
</template>

<script>
export default {
  name: 'sunset',
};
</script>

<style lang="scss">
  $clouds-color: #feffd5;
  $sky-color: #3e4b69;
  $sea-color: #8ca6fb;
  $sunset-sky-color: #e2645a;
  $sun-color: #f4d06d;
  $sun-color-end: #eca565;

  $viewport-width: 500px;
  $viewport-height: 400px;

  $number-of-lines: 10;
  $number-of-spacings: $number-of-lines - 1;
  $spacing: 20px;
  $remaining-height: $viewport-height - $number-of-spacings * $spacing;

  $sky-line-width-ratios: 0.2 0.5 0.68 0.8 0.9 1 0.9 0.5 0.4 0.1;
  $sky-line-height-ratios: 1 1.3 1.8 2.5 3.3 3.8 3.3 1.1 0.8 0.7;
  $sky-line-height-ratios-sum: 0;

  @each $item in $sky-line-height-ratios {
    $sky-line-height-ratios-sum: $sky-line-height-ratios-sum + $item;
  }

  $sky-line-height-ratios-unit: $remaining-height / $sky-line-height-ratios-sum;

  .sunset {
    width: $viewport-width;
    height: $viewport-height;
    position: relative;

    .sun {
      $sun-width: $viewport-width * 0.53;
      $sun-height: $sun-width / 2;

      width: $sun-width;
      height: $sun-height;
      border-top-left-radius: $sun-width * 2;
      border-top-right-radius: $sun-width * 2;

      background: linear-gradient(to bottom,
                  $sun-color, $sun-color 30%,
                  $sun-color-end 74%, $sunset-sky-color);
      left: 50%;
      margin-left: -$sun-width / 2;
      bottom: 0%;
      position: absolute;
    }

    $big-cloud-width: 60px;
    $big-cloud-height: $big-cloud-width / 2;

    $small-cloud-width: 35px;
    $small-cloud-height: $small-cloud-width / 2;

    .cloud {
      position: absolute;
      z-index: 999;
      display: inline-flex;
      align-items: flex-end;
      bottom: 0;

      animation: cloud-move;
      animation-timing-function: linear;
      animation-iteration-count: infinite;

      &::before,
      &::after {
        content: '';
        width: 0;
        height: 0;
        background: $clouds-color;
      }

      &::before {
        display: block;
        width: $big-cloud-width;
        height: $big-cloud-height;
        border-top-left-radius: $big-cloud-width * 2;
        border-top-right-radius: $big-cloud-width * 2;
      }

      &--reverse {
        flex-direction: row-reverse;
      }

      &--double {
        &::before {
        }

        &::after {
          display: block;
          width: $small-cloud-width;
          height: $small-cloud-height;
          border-top-left-radius: $small-cloud-width * 2;
          border-top-right-radius: $small-cloud-width * 2;
        }
      }

      &--1 {
        left: 35%;
        animation-duration: 10s;
      }

      &--2 {
        left: 60%;
        transform: scale(1.5);
        transform-origin: bottom center;
        animation-direction: reverse;
        animation-duration: 11s;
      }

      &--3 {
        left: 40%;
        bottom: 200%;
        transform: scale(1.4);
        transform-origin: bottom center;
        animation-duration: 14s;
      }

      &--4 {
        left: 40%;
        bottom: 100%;
        transform: scale(1.2);
        transform-origin: bottom center;
        animation-direction: reverse;
        animation-duration: 12s;
      }

      &--5 {
        left: 23%;
        bottom: 40%;
        transform: scale(1.5);
        transform-origin: bottom center;
        animation-duration: 13s;
      }
    }

    .background-line {
      margin-left: auto;
      margin-right: auto;
      width: 100%;
      margin-bottom: $spacing;

      &--sky {
        background: $sunset-sky-color;
      }

      &--sea {
        background: $sea-color;
      }

      &--contains-sun,
      &--has-clouds {
        position: relative;
      }

      @for $i from 1 through $number-of-lines {
        &:nth-child(#{$i}) {
          width: $viewport-width * nth($sky-line-width-ratios, $i);
          height: $sky-line-height-ratios-unit * nth($sky-line-height-ratios, $i);
          border-radius: $sky-line-height-ratios-unit * nth($sky-line-height-ratios, $i);

          @if $i != 6 {
            animation: line-move;
            animation-duration: 4s;
            animation-timing-function: ease-in-out;
            animation-iteration-count: infinite;
            animation-direction: alternate;

            @if $i % 2 == 0 {
              animation-direction: alternate-reverse;
            }
          }
        }
      }

      &:last-child {
        margin-bottom: 0;
      }
    }
  }

  @keyframes line-move {
    from {
      transform: translateX(0);
    }

    to {
      transform: translateX(-10px);
    }
  }

  @keyframes cloud-move {
    0% {
      margin-left: -50%;
      opacity: 0;
    }

    33% {
      margin-left: -17%;
      opacity: 1;
    }

    66% {
      margin-left: 17%;
      opacity: 1;
    }

    100% {
      margin-left: 50%;
      opacity: 0;
    }
  }
</style>
