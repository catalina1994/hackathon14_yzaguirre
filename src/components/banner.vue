<template>
    <div class="banner py-1 px-1">
        <div class="banner__caption">
            <p class=" my-m1">{{subtitle}}</p>
            <h2 class="banner__title">
                {{title}}
            </h2>
        </div>
    </div>
</template>
<script>
    export default {
        name:"banner",
        props: {
            title: String,
            subtitle: String
        }
    }
</script>
<style lang="scss">
/*colores*/
$color-principal: #ff3773;
$color-secundary: #e01876;
$color-third:#fff;
 
$color-auxiliar:#cf0664;
$color-auxiliar-secundary:rgb(64, 160, 207);

/*font-weight*/

$font-bold:600;
$font-normal:400;
$font-light:300;

/*font-size*/
$font-size-small:14px;
$font-size:16px;
$font-size-large:22px;
$font-size-xlarge:36px;

/*font-family*/
$font-roboto: Arial, Helvetica, sans-serif ;
$font-helvetica: Helvetica, Arial, sans-serif;

//mixins
@mixin mediaQ($breakpoint) {
    @media screen and (min-width: $breakpoint){
      @content;
    }
  }
.banner{
    background-color: $color-secundary;

    &__caption{
        padding: 1.5em  3em  1.5em;
        color: $color-third;
        text-align: center;
        
    }
    &__title{
        font-size:$font-size-xlarge ;
    }
}
</style>