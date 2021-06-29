<template>
  <div class="container">
    <div class="block" :class="{animate:animateBlock}"></div>
    <button @click="animatedBlock">Animate</button>
  </div>
  <div class="container">
    <transition
     name="para" 
      @before-enter="beforeEnter"
      @before-leave="beforeLeave" 
      @enter="enter" 
      @after-enter="afterEnter"
      @leave="leave"
      @after-leave="afterLeave"
      >
    <p v-if="paraIsVisible">This is only sometimes visible...</p>
    </transition>
    <button @click="toggleParagraph">Toggle Paragraph</button>
  </div>
  
    <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>
  <div class="container">
    <transition name="fade-button" mode="out-in">
        <button @click="showUsers" v-if="!usersAreVisible">Show Users</button>
        <button @click="hideUsers" v-else>Hide Users</button>
    </transition>
  </div>
</template>  

<script>
export default {
  data() {
    return { 
      animateBlock:false,
      dialogIsVisible: false,
      paraIsVisible:false,
      usersAreVisible:false
       };
  },
  methods: {
    leave(el){
      console.log('Leave')
      console.log(el)
    }
    ,
    afterLeave(el){
      console.log('after Leave')
      console.log(el)
    }
    ,
    afterEnter(el){
      console.log('after Enter...')
      console.log(el)
    }
    ,
    enter(el){
      console.log('enter')
      console.log(el)
    }
    ,
  beforeLeave(el){
    console.log('beforeLeave()')
    console.log(el)
  }
,
    beforeEnter(el){
      console.log('beforeEnter()')
      console.log(el)
    }
    ,
    showUsers(){
      this.usersAreVisible=true
    },
    hideUsers(){
      this.usersAreVisible=false
    }
    ,
    toggleParagraph(){
      this.paraIsVisible=!this.paraIsVisible
    },
    animatedBlock(){
      this.animateBlock= !this.animateBlock
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition: transform 1.3s ease-out; */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.animate{
  /* transform: translateX(-150px); */
  animation: slide-scale 1s ease-out forwards;

}
/* .v-enter-from{
  /* opacity: 0;
  transform: translateY(-30px); */
/* }  */
.para-enter-active{
  animation: slide-scale 2s ease-out;
}
/* .v-enter-to{
  /* opacity: 1;
  transform: translateY(); */
/* }  */
/* .v-leave-from{
  opacity: 1;
  transform: translateY(0);
} */
.para-leave-active{
 animation: slide-scale 0.3s ease-in;
}
/* .v-leave-to{
  opacity: 0;
  transform: translateY(-30px);
} */

.fade-button-enter-from,
.fade-button-leave-to{
  opacity: 0;
}
.fade-button-enter-active{
  transition: opacity 0.3s ease-out;
}
.fade-button-leave-active{
  transition: opacity 0.3s ease-in;
}
.fade-button-enter-to,
.fade-button-leave-from
{
  opacity: 1;
}

@keyframes slide-scale{
  0%{
    transform: translateX(0) scale(1);

  }
  70%{
    transform: translateX(-120px) scale(1.5);
  }
  100%{
    transform: translateX(-150px) scale(0.5);
  }
}

</style>