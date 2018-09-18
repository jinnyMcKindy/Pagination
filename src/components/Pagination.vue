<template>
  <div class="container">
    <results class="srch-results" v-for="result in visible" 
            :key="result.id"
            :title="result.title"
            :description="result.description"
            :url="result.url"
         v-bind:href="result.url"> 
    </results>
    <div class="c2c-pagination">
         <dot-component 
            :Max="leftMax" 
            v-on:click-dots="clickDots" 
            value="left">
         </dot-component>
         <page-component 
            v-for="(page, index) in range(first, visiblePages)" 
                     :key="page.id"
                     v-on:navigate-of="navigate(page)" 
                     :page="page" 
                     :class="['page-' + page]"
         >
        </page-component>
          <dot-component v-bind:Max="rightMax" v-on:click-dots="clickDots" value="right"></dot-component>
     </div>
  </div>
</template>

<script>

import Results from './Results';
import PageComponent from './PageComponent';
import DotComponent from './DotComponent';

export default {
  name: 'Pagination',
  props:  [],
  data: function () {
    return {
       text : "",
       shownotfound: false,
       results : {},  //all results
       size : 0,
       pages: 0,
       visiblePages: 0,
       perPage: 4,
       visible : {}, //visible results, 
       rightMax: false,
       leftMax: false,
       first: 1,
       dirty: true,
       oldUrl : "",
       maxAmountOfPages : 5
    }
  },
    components: {
          Results, PageComponent, DotComponent
    },
    created : function(){
        var json = [
            {title : "Title1", description : "Description", url : "www.google.com"},
            {title : "Title2", description : "Description", url : "www.google.com"},
            {title : "Title3", description : "Description", url : "www.google.com"},
            {title : "Title4", description : "Description", url : "www.google.com"},
            {title : "Title5", description : "Description", url : "www.google.com"},
            {title : "Title6", description : "Description", url : "www.google.com"},
            {title : "Title7", description : "Description", url : "www.google.com"},
            {title : "Title8", description : "Description", url : "www.google.com"},
            {title : "Title9", description : "Description", url : "www.google.com"},
            {title : "Title10", description : "Description", url : "www.google.com"},
            {title : "title11", description : "Description", url : "www.google.com"},
            {title : "Title12", description : "Description", url : "www.google.com"},
            {title : "Title13", description : "Description", url : "www.google.com"},
            {title : "Title14", description : "Description", url : "www.google.com"},
            {title : "Title15", description : "Description", url : "www.google.com"},
            {title : "Title16", description : "Description", url : "www.google.com"},
            {title : "Title17", description : "Description", url : "www.google.com"},
            {title : "Title18", description : "Description", url : "www.google.com"},
            {title : "Title19", description : "Description", url : "www.google.com"},
            {title : "Title20", description : "Description", url : "www.google.com"},
            {title : "Title21", description : "Description", url : "www.google.com"},
            {title : "Title22", description : "Description", url : "www.google.com"},
            {title : "Title23", description : "Description", url : "www.google.com"},
            {title : "Title24", description : "Description", url : "www.google.com"},
            {title : "Title25", description : "Description", url : "www.google.com"},
            {title : "Title26", description : "Description", url : "www.google.com"},
            {title : "Title27", description : "Description", url : "www.google.com"},
            {title : "Title28", description : "Description", url : "www.google.com"},
            {title : "Title29", description : "Description", url : "www.google.com"},
            {title : "Title30", description : "Description", url : "www.google.com"},
            {title : "Title31", description : "Description", url : "www.google.com"},
            {title : "Title32", description : "Description", url : "www.google.com"},
        ];
        this.results = json;
        this.size = json.length; //количество найденных совпадений
        this.setPages(json.length); //высчитываем кол-во страниц для пагинации
    },
    methods: { 
        setPages : function(len){
            if( len <= this.perPage ){ //если вывод списка помещается на 1 страницу
               this.pages = 0; //цифры пагинации
               this.visible = this.results; //выводим результаты
               return;
            }
            var pages = Math.ceil( len/ this.perPage );
            this.pages = pages;
            this.navigate(1); //навигация с 1 страницы
        },
        navigate : function ( indexPage ) {
            var end = indexPage-1; //если кликнутый оффсет равен 2, то обрезаем с 10, если 1, то с 0
            var offset = this.perPage * end; //находим индекс, с которого обрезаем массив
            this.visible = Object.values( this.results ).splice( offset, this.perPage ); //выводим результаты
            setTimeout(() => {
                var x = document.getElementsByClassName("page");
                var i;
                for (i = 0; i < x.length; i++) {
                    x[i].classList.remove("active");
                    var ind = "page-"+indexPage;
                    if( x[i].classList.contains( ind ) ){
                            x[i].classList.add("active");
                    }
                }
            });
            if(this.dirty) this.checkDots();   
        },
        checkDots(){
            if( this.pages <= this.maxAmountOfPages ) {
                this.visiblePages = this.pages; 
            }
            else {
                this.visiblePages = this.maxAmountOfPages;
                this.rightMax = true; 
                this.leftMax = false;
            }
        },
        clickDots: function (dotName){
            this.dirty = false;
            this.leftMax = true;
            this.rightMax = true; 
            let first, last, obj;
            dotName === "right" ?  obj = this.rightDir() : obj = this.leftDir();
            [ this.first, this.visiblePages ] = obj;
            this.navigate( obj[0] );
        },
        rightDir: function(){
            let first, last, obj;
            last = this.visiblePages + this.maxAmountOfPages;
            first = this.visiblePages;
            if( last >= this.pages ){ 
                last =  this.pages;
                this.rightMax = false; 
            }
            obj = [ first, last ];
            return obj;
        },
        leftDir: function(){
            let first, last, obj;
            last = this.first;
            first = last - this.maxAmountOfPages;
            if(first === 1) this.leftMax = false; 
            if(first <= 0){
                   first = 1;
                   this.leftMax = false; 
            }
            obj = [ first, last ];
            return obj;
        },
        range: function(min,max){
            var array = [],
                j = 0;
                for(var i = min; i <= max; i++){
                    array[j] = i;
                    j++;
            }
            return array;
        }
    } 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.page.active {
    color: red;
}
.container {
    margin: auto;
    max-width: 700px;
}
.c2c-pagination {
    display: flex;
    justify-content: center;
    margin-top: 10px;
}
.page {
    padding: 10px;
    cursor: pointer;
}
.c2c-dot {
    cursor: pointer;
}
</style>
