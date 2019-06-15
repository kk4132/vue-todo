<template>
  <div id="app">
    <Header></Header>
    <todo></todo>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from './views/Header'
import todo from './views/todo'
import Footer from './views/Footer'
export default {
  data(){
    return{

    }
  },
  components:{
    Header,
    todo,
    Footer
  }
}
</script>


<style lang="scss">
*{
  padding: 0;
  margin: 0;
}
li{
  list-style-type: none;
}
body{
  background: url(./assets/images/bg.jpeg) no-repeat; 
  max-width: 100%;  
  max-height: 100%;
  background-size:100% 920px; 
}
#app{
  width: 600px;
  margin: 0 auto;
  height: 900px;
  border: 1px solid #333;
}
</style>
