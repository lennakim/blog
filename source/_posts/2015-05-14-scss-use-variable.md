title: 在scss中使用变量
date: 2015-05-14 15:33:48
tags: [scss]
---


``` scss

//定義方法 animation-delay-n
@mixin animation-delay-seconds($n){
  &:nth-child(#{$n}){
    animation-delay: #{$n*2}s;
  }
}

div {
  @include animation-delay-seconds(1);
  @include animation-delay-seconds(3);
  @include animation-delay-seconds(5);
}

```

生成的css 如下:

``` css
div:nth-child(1) {
  animation-delay: 2s;
}

div:nth-child(3) {
  animation-delay: 6s;
}

div:nth-child(5) {
  animation-delay: 10s;
}

```

### 资料

[use-nth-child-value-as-a-sass-variable](http://stackoverflow.com/a/20121376/1240067)

[select-every-nth-element-in-css](http://stackoverflow.com/a/3462301/1240067)

[sass-meister](http://sassmeister.com/)
