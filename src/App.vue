<template>
  <div>
    <modal id="modalEliminar">
          <p class="my-2 mx-2">Esta seguro que quiere eliminar a esta mascota.</p>
          <div class="mb-1">
                <button class="btn borrar mr-1">Aceptar</button>
                <button class="btn btn-line">Cancelar</button>
          </div>
    </modal>
    <modal id="modalFormAdd">
            <div class="form mb-1">
                <h4 class="mb-1 text-center" >Agregar video</h4>
                <article class="flex align-center">
                    <label for="title">Titulo</label>
                    <input type="text" name="title" id="title" value="">   
                </article>
                <article class="flex align-center">
                    <label for="categoria"> Categoria</label>
                    <input type="text" name="categoria" id="categoria">
                </article>
                <article class="flex align-center">
                    <label for="description"> Descripion</label>
                    <input type="text" name="description" id="description">
                </article>
            </div>
            <div class="mb-1">
                <input class="btn agregar" type="submit" value="Agregar">
                <button class="btn btn-line">Cancelar</button>
            </div>
    </modal>
    
    <banner subtitle="Hacktahon 14" title="VIDEO CRUD"></banner>
    <section class="my-1">
        <div class="container">
            <div class="flex mb-2 justify-between">
                <h2 class="">VIDEO CRUD </h2>
                <button @click="agregarVideo" class="btn "> Agregar Video</button>
            </div>
            <div id="listDogs" class="flex justify-between wrap" @click="eliminarVideo">
               <article class="card" v-for='(video, index) in videos' :key='index'>
                 <div class="card__img">
                        <img :src="video.img" alt="">
                    </div>
                    <div class="card__caption">
                        <h3 class="card__title">
                            {{video.title}}
                        </h3>
                        <h4 class="mb-1">{{video.categoria}}</h4>
                        <p class="mb-1">{{video.Descricpcion}}</p>
                    <div class="card__action">
                        <button class="btn delete mr-1" >Eliminar</button>
                        <button class="btn btn-line">Editar</button>
                    </div>
                    </div>
               </article>
            </div>
        </div>
    </section>
  </div>
</template>

<script>
import banner from './components/banner';
import modal from './components/modal'

export default {
  name: 'App',
  components: {
    banner,
    modal
  },
  data(){
    return {
      videos:[]
    }
  },

  mounted(){//es un metodo de la instancia
        const data = fetch('http://localhost:3000/video')
        .then(info =>{
            return info.json();
        })
        .then(video =>{
            this.videos = video
        })
        
    },
  methods:{
      eliminarVideo(e){
        const modal = document.getElementById('modalEliminar')
        if(e.target.classList.contains(`delete`)){
               const video = e.target.parentElement.parentElement.parentElement
                modal.classList.add('modal--show')
                modal.addEventListener('click', (e)=>{
                    e.preventDefault()
                    if(e.target.classList.contains('borrar')){
                       video.remove()
                        modal.classList.remove('modal--show')
                    }
                    if(e.target.classList.contains('btn-line')){
                        modal.classList.remove('modal--show')
                    }
                    if(e.target.classList.contains('btnClose')){
                        modal.classList.remove('modal--show')
                    }
                    console.log(video)
                })
           }  
       },
      agregarVideo(e){
        const modalFormAdd = document.getElementById('modalFormAdd')
        e.preventDefault()
        modalFormAdd.classList.add('modal--show')
        modalFormAdd.addEventListener('click', (e) =>{
          e.preventDefault()
          if(e.target.classList.contains('btn-line')){
              modalFormAdd.classList.remove('modal--show')
                    }
          if(e.target.classList.contains('btnClose')){
            modalFormAdd.classList.remove('modal--show')
          }
          if(e.target.classList.contains('agregar')){
            modalFormAdd.classList.remove('modal--show')
          }
        })
      }
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
  *, 
*::after,
*::before{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

ul{
    list-style: none;
}
a{
    text-decoration: none;
}
.text-center{
    text-align: center;
}
body{
    font-family: $font-roboto;
    background-color: #fff;
}
.img-responsive{
    max-width: 100%;
    display: block;
}
.material-icons{
    cursor: pointer;
}

.flex{
    display: flex;
    &.direction-column{
        flex-direction: column;
    }
    &.justify-between{
        justify-content: space-between;
    }
    &.justify-end{
        justify-content: flex-end;
    }
    &.justify-center{
        justify-content: center;
    }
    &.align-center{
        align-items: center;
    }
    &.wrap{
        flex-wrap: wrap;
    }
}
.grid{
    display: grid;
}



.mx-1{
    margin-left: 1em;
    margin-right: 1em;
}
.mx-2{
    margin-left: 2em;
    margin-right: 2em;
}

.my-m1{
    margin-top: .5em;
    margin-bottom: .5em;
}
.my-1{
    margin-top: 1em;
    margin-bottom: 1em;
}
.my-2{
    margin-top: 2em;
    margin-bottom: 2em;
}
.mb-1{
    margin-bottom: 1em;
}
.mb-2{
    margin-bottom: 2em;
}
.mr-1{
    margin-right: 1em;
}

.px-1{
    padding-left: 1em;
    padding-right: 1em;
}
.py-1{
    padding-top: 1em;
    padding-bottom: 1em;
}
.pb-1{
    padding-bottom: 1em;
}
.pb-2{
    padding-bottom: 2em;
}

.container{
    width: 100%;
    margin: 0 auto;
    padding-right: 15px;
    padding-left: 15px;

    @media (min-width: 1366px){
        width: 1100px;
    }
    @media (min-width: 1600px){
        width: 1200px;
    }
}
.btn{

    cursor: pointer;
    padding: .5em 1.2em;
    border: 1px solid $color-secundary;
    background-color:$color-secundary;
    color:#fff;
    border-radius: 4px;
    transition: background-color .4s, border .4s ;
    margin-bottom:.4em;
    &.btn-line{
        border: 1px solid $color-secundary;
        background-color: #fff;
        color:$color-secundary;
        transition: background-color .5s, color .5s, border .5s  ;
        &:hover{
            color:#fff;
        }
    }
    &:hover{
        background-color:$color-auxiliar;
        border: 1px solid $color-auxiliar;
    }
}
.card{
    padding: 1em 1em;
    background-color: rgb(252, 252, 252);
    margin: 0 auto;
    margin-bottom: 1.2em;
    border-radius:6px;
    box-shadow: 1px 1px 4px rgba(59, 59, 59, 0.363);
    transition: transform .5s ;
    text-align: center;
    width: 90%;
    @include mediaQ(576px){
        width: 31%;
    }
    @include mediaQ(972px){
        width: 23.5%;
    }
    &__title{
        margin :0;
        margin-bottom: .7em;
        color: rgb(32, 32, 32);
        text-align: center;
    }
    &__img{
        overflow: hidden;
        margin: 0 auto;
        margin-bottom: 1em;
        img{
            max-height: 100%;
            display: block;
            margin: 0 auto;
        }
    }
    &__list{
        font-size:$font-size-small;
        margin-bottom: 1em;
    }

    &:hover{
        transform: scale(1.1);
        box-shadow: 1px 1px 12px 3px rgba(59, 59, 59, 0.363);
        z-index: 1;

    }
}
.form{
    text-align:left;
    padding: 0 2em;
    label{
        width: 100px;
        text-align: right;
        margin-right: 1em;
    }
    input{
        border: none;
        padding:.5em .5em;
        background-color: rgb(242, 242, 243);
        margin-bottom: .5em;

    }
}
</style>
