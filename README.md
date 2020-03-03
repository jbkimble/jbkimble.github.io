# kimble.io - my website

Pug SCSSResult
EDIT ON
@import "bourbon";

$box-size: 480px;
$rings: 30;
$duration: 2.5s;
$lagdelay: 1.25;

body {
  background-color: black;
}

.container {
  width: $box-size;
  height: $box-size;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -($box-size / 2);
  margin-left: -($box-size / 2);

  .ring {
    margin: 0 auto;
    position: absolute;
    text-align: center;
  }
}

@for $i from 1 through $rings {
  $perc: (($rings - $i) / $rings);

  @include keyframes(el-animate-#{$i}) {
    0% {
      border-color: rgb(255 * $perc, 255 * $perc, 255 * $perc);
      transform: rotate(0deg);
    }
    25% {
      border-color: rgb(255 * (1 - $perc), 125 * $perc, 255 * (1 - $perc));
      transform: rotate(45deg);
    }
    75% {
      border-color: rgb(125 * $perc, 255 * (1 - $perc), 255 * $perc);
      transform: rotate(135deg);
    }
    100%{
      border-color: rgb(255 * $perc, 255 * $perc, 255 * $perc);
      transform: rotate(180deg);
    }
  }

  .ring.el-#{$i} {
    $size: $box-size * $perc;

    border: 2px solid black;
    border-color: rgb(255 * $perc, 255 * $perc, 255 * $perc);
    left: ($box-size / 2) - ($size / 2);
    top: ($box-size / 2) - ($size / 2);
    width: $size;
    height: $size;
    border-radius: ($size * 0.35);

    @include animation(el-animate-#{$i} $duration linear);
    @include animation-delay($lagdelay * ($duration * $perc));
    @include animation-iteration-count(infinite);
  }
}
