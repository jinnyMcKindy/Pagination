
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
  </div>
</template>

<script>



export default {
  name: 'Pagination',
  props:  ["msg"],
  data: function () {
    return {
       text : "",
       shownotfound: false,
       results : {},  //all results
       size : 0,
       pages: 0,
       visiblePages: 0,
       perPage: perPage,
       visible : {}, //visible results, 
       rightMax: false,
       leftMax: false,
       first: 1,
       dirty: true,
       loader : false,
       oldUrl : ""   
    }
  },
  components: {
        //Results, PageComponent, DotComponent
  },
    methods: { 
        setResults : function( json ){
            this.results = json;
            this.size = json.length; //количество найденных совпадений
            this.setPages(json.length); //высчитываем кол-во страниц для пагинации
            this.loader = false;
        },
        setPages : function(len){
            if( len <= this.perPage ){ //если вывод списка помещается на 1 страницу
               vm2.pagination = false;
               this.pages = 0; //цифры пагинации
               this.visible = this.results; //выводим результаты
               return;
            }
            vm2.pagination = true;
            var pages = Math.ceil( len/ this.perPage );
            this.pages = pages;
            this.navigate(1); //навигация с 1 страницы
        },
        navigate : function ( indexPage ) {
            var end = indexPage-1; //если кликнутый оффсет равен 2, то обрезаем с 10, если 1, то с 0
            var offset = this.perPage * end; //находим индекс, с которого обрезаем массив
            this.visible = Object.values( this.results ).splice( offset, this.perPage ); //выводим результаты
            setTimeout(function(){
                $(".page").removeClass("active");
                $(".page-"+indexPage).addClass("active");
            });
            if(this.dirty) this.checkDots();   
        },
        checkDots(){
            if( this.pages <= maxAmountOfPages ) {
                this.visiblePages = this.pages; 
            }
            else {
                this.visiblePages = maxAmountOfPages;
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
            last = this.visiblePages + maxAmountOfPages;
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
            first = last - maxAmountOfPages;
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
</style>
