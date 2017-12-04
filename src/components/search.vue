<template>
<div id="search">
    <input type="search" value="" ref="message" v-on:keyup.enter="click" id="busqueda" placeholder="type keyword(s) here" />
    <button type="submit" v-on:click="click" class="btn btn-primary">Search</button>
    <div class="row">
    <div v-for="foto in imagenes" >
        <div class="col-8">
        <a><img class="image" :id="foto.id" :width="200" :src="foto.urls.small"  v-on:click="zoom(foto.id)" ></a>
        </div>
        </div>
    </div>
</div> 

</template>
<script>
import axios from "axios";
export default {
    name: 'search',
    data () {
        return {
       imagenes:[],
   
        }
    },
    methods:{
          getImagenes:function(){
        console.log(this.imagenes);
        return this.imagenes;
    },

        click:function(){
        var url = 'https://api.unsplash.com';
        var app_id = 'a2ff151436d46fe84a083fbee42db71edfe34836611f8fa2c2f7a804aa685db6';
        var secret = 'cb9030ebd2d85e29f1eff60551263fdca8df5f2c832ddfb3a518c6ba52dfcd4c';
        var added_to_url = '/search/photos/';
        var keyword = document.getElementById("busqueda").value;
        var added_query = '?query='
        var self = this;
        axios({ 
                method: 'get',
                url: url + added_to_url + added_query + keyword, 
                headers: {
                'Accept-Version': 'v1',
                'Authorization': 'Client-ID '+ app_id
                }
               }).then((response) => { 
            if (response){
                console.log(response);
                self.imagenes = response.data.results;
            }
             });
    },
     zoom:function(id){
        var el = document.getElementById(id);
        console.log(el.width);
        
        if (el.width == "200"){  
            console.log("aui");
             el.width = "800";
        }else{
            console.log("otro");
             el.width = "200";
        }
        console.log(el.width);
    },
     

    }


}

</script>
<style>

.full {
  width: 100%;
  height: auto;
}
img {

  border-radius: 2px;
  box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.5);
  transition: width 1s;
}
img:hover {
  cursor: pointer;
}

 #search {
     position: fixed; 
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
  
}
 #search input[type="search"] {
  
  
    color: rgb(255, 255, 255);
    background: rgba(0, 0, 0, 0);
    font-size: 60px;
    font-weight: 300;
    text-align: center;
    border: 0px;
    margin: 0px auto;
    padding-right: 30px;
    outline: none;
        margin-left: 30%;
} 
#search .btn {
    left: 50%;
    margin-top: -24px;
    margin-left: -45px;
} 

</style>