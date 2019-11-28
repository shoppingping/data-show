<template>

  <div class="background">
    
    <div class="card">
      <div class="photo"></div>
      <h2>STEPS</h2>
      <p>THIS WEEK</p>
      <div class="chart">
        <div class="bar bar1"><span>20,000</span></div>
        <div class="bar bar2"><span>10,000</span></div>
        <div class="bar bar3"><span>15,000</span></div>
        <div class="bar bar4"><span>24,000</span></div>
        <div class="bar bar5"><span>7,000</span></div>
        <div class="bar bar6"><span>7,000</span></div>
        <!-- <div class="bar bar7"><span>10,000</span></div> -->
      </div>
      <h3>核心交易量 93,000</h3>
    </div>
    
    <!-- <div class="info">Click to toggle details view</div> -->
  </div>

</template>


<script>


export default {
  // name: 'info-card',
  // components: {
  //   InfoCard,
  // },
  data() {
    return {};
  },

  mounted(){
    let body= document.body;
    let tilted = false;

    // let toggleTilt = function()
    // {
      tilted = !tilted;
      
      if(tilted) body.classList.add('details');
      else body.classList.remove('details');
    // }

    // body.addEventListener('click', toggleTilt);
    // body.addEventListener('touchstart', toggleTilt);
    // if(location.pathname.match(/fullcpgrid/i)) setTimeout(toggleTilt, 1000);
  },

  method:{

  },
}
</script>


<style scoped lang="scss">
// @import url('https://fonts.googleapis.com/css?family=Asar|Oxygen');

@mixin center
{
  display: flex;
  align-items: center;
  justify-content: center;
}

$size: 25px;
$size-big: 40px;
$layer-gap: 30px;


.card
{
  background-color: rgba(0,0,0,.2);
  width: 450px;
  // height: 300px;
  border-radius: 10px;
  perspective: 1500;
  transition: transform 0.5s ease-in-out, box-shadow 0.5s ease-in-out;
  @include center;
  flex-direction: column;
  transform-style: preserve-3d;
  box-shadow: 5px 5px 24px 0px rgba(0,0,0,0.2);

  border: rgba(0,0,0,1) solid 1px;
  border-radius: .3em .3em .3em .3em;
  
  @media (min-height: 600px) 
  {
    // width: 400px;
    width: 60%;
    // height: 550px;
  }
  
  
  h2, h3, P
  {
    transform: translateZ(2px);
    color: white;
    font-size: 30px;
    line-height: 30px;
    margin: 0;
    font-weight: 300;
    padding: 0;
    transition: transform 0.5s ease-in-out, opacity 0.5s ease-in-out;
    
    @media (min-height: 600px) 
    {
      font-size: 40px;
      line-height: 40px;
    }
  }
  
  h2
  {
    margin: 20px 0 0 0;
  } 
  
  h3
  {
    margin: 10px 0 40px 0;
    
    @media (min-height: 600px) 
    {
      margin: 20px 0 40px 0;
    }
  }
  
  P
  {
    margin: 0px 0 30px 0;
    font-size: 16px;
    
    @media (min-height: 600px) 
    {
      margin: 0px 0 40px 0;
      font-size: 21px;
    }
  }
  
  .chart
  {
    @include center;
    transform-style: preserve-3d;
    transform: translateZ(2px);
    transition: transform 0.5s ease-in-out;
  }
  
  // .photo
  // {
  //   position: absolute;
  //   transform: translateZ(1px);
  //   top: 0;
  //   left: 0;
  //   right: 0;
  //   bottom: 0;
  //   background: url('https://source.unsplash.com/kpAXYoXSeuY/600x600') no-repeat center center; 
  //     background-size: cover;
  //   border-radius: 10px;
  //   transition: transform 0.5s ease-in-out;
  //   overflow: hidden;
    
  //   &:after
  //   {
  //     position: absolute;
  //     content: ' ';
  //     display: block;
  //     top: 0;
  //     right: 0;
  //     bottom: 0;
  //     left: 0;
  //     background-color: rgba(0, 0, 0, 0.2);
  //     transition: background-color 0.5s ease-in-out;
  //   }
  // }
  
  .bar
  {
    will-change: height;
    width: $size;
    height: 1px;
    background-color: white;
    transform: translateX(-($size / 2)) rotateX(-90deg) rotateY(-45deg);
    transform-origin: 100% 100%;
    transition: height 0.5s ease-in-out, margin 0.5s ease-in-out, transform 0.5s ease-in-out;
    transform-style: preserve-3d;
    margin: 6px;
    position: relative;
    background: linear-gradient(to bottom, #feffff 0%, #ddf1f9 0%, #a0d8ef 100%);
      
    @media (min-height: 600px) 
    {
      margin: 10px;
      width: $size-big;
      transform: translateX(-($size-big / 2)) rotateX(-90deg) rotateY(-45deg);
    }
    
    &:after
    {
      display: block;
      content: '';
      height: 100%;
      width: $size;
      position: absolute;
      top: 0;
      right: -$size;
      background-color: grey;
      transform: rotateY(90deg);
      transform-origin: 0% 50%;
      
      @media (min-height: 600px) 
      {
        width: $size-big;
        right: -$size-big;
      }
      
      background: linear-gradient(to bottom, #feffff 0%,#85d7f7 0%,#4c8596 100%);
    }
    
    &:before
    {
      font-family: 'Oxygen', sans-serif;
      display: block;
      content: '';
      height: $size;
      width: $size;
      position: absolute;
      top: -$size;
      left: 0;
      background-color: white;
      transform: rotateX(90deg);
      transform-origin: 0% 100%;
      color: white;
      text-align: center;
      font-size: 10px;
      line-height: 14px;
      padding: 0;
      
      @media (min-height: 600px) 
      {
        width: $size-big;
        height: $size-big;
        top: -$size-big;
        font-size: 12px;
        line-height: 18px;
      }
      
      transition: color 0.3s ease-in-out;
      
    }
    
    &.bar1:before { content: 'M' }
    &.bar2:before { content: 'T' }
    &.bar3:before { content: 'W' }
    &.bar4:before { content: 'T' }
    &.bar5:before { content: 'F' }
    &.bar6:before { content: 'S' }
    &.bar7:before { content: 'S' }

    &.bar1:after { content: 'E商宝' }
    &.bar2:after { content: '网上银行' }
    &.bar3:after { content: '手机银行' }
    &.bar4:after { content: '柜面银行' }
    &.bar5:after { content: '超级网银' }
    &.bar6:after { content: '其它' }
    &.bar7:after { content: 'S' }
    
    span
    {
      font-family: 'Oxygen', sans-serif;
      position: absolute;
      //transform: rotateY(-45deg);
      transform: rotateZ(-90deg);
      border-radius: 2px;
      transform-origin: 0% 100%;
      top: 20px;
      white-space: nowrap;
      text-align: right;
      left: $size + 3px;
    //  background-color: rgba(255,255,255,0.75);
      padding: 5px;
      color: black;
      font-size: 10px;
      opacity: 0;
      transition: opacity 0.5s ease-in-out;
      
      @media (min-height: 600px) 
      {
        top: 25px;
        left: $size-big - 0px;
        font-size: 13px;
      }
    }
    
  }
}

.details
{
  .card
  {
    transform: rotateX(60deg) translateY(20px);
    box-shadow: 0px 30px 40px 0px rgba(0,0,0,0.75);
    
    .chart
    {
      transform: translateZ($layer-gap * 2) translatey(50px);
    }
    
    .bar
    {
      transform: translateX(-($size / 2)) rotateX(-90deg) rotateY(-45deg);
        
      @media (min-height: 600px) 
      {
        transform: translateX(-($size-big / 2)) rotateX(-90deg) rotateY(-45deg);
      }
      
      &.bar1 { height: 200px * 0.75; transition-delay: 0.3s; margin-top: -200px * 0.75;}
      &.bar2 { height: 100px * 0.75; transition-delay: 0.2s; margin-top: -100px * 0.75;}
      &.bar3 { height: 150px * 0.75; transition-delay: 0.1s; margin-top: -150px * 0.75;}
      &.bar4 { height: 240px * 0.75; transition-delay: 0s; margin-top: -240px * 0.75;}
      &.bar5 { height: 70px * 0.75; transition-delay: 0.1s; margin-top: -70px * 0.75;}
      &.bar6 { height: 70px * 0.75; transition-delay: 0.2s; margin-top: -70px * 0.75;}
      &.bar7 { height: 100px * 0.75; transition-delay: 0.3s; margin-top: -100px * 0.75;}
      
      span
      {
        opacity: 1;
        transition-delay: 0.3s;
      }
        
      &:before
      {
        color: black;
      }
    }
    
    .photo
    { 
      transform: translateZ($layer-gap);
      
      &:after
      {
        background-color: rgba(0, 50, 100, 0.8);
      }
    }
    
    h2, h3
    {
      
    }
    
    h2
    {
      opacity: 0;
      transform: translateZ($layer-gap * 2) translateY(-100px);
    }
    
    p
    {
      opacity: 0;
      transform: translateZ($layer-gap * 2) translateY(-80px);
    }
    
    h3
    {
      transform: translateZ($layer-gap * 3) translateY(100px);
    }
    
    
  }
}

.background 
{
  width: 100%;
  height: 100%;
  
  @include center;
  
  
  position: relative;
  // background: linear-gradient(120deg, rgba(50, 150, 100, 0.4), rgba(0, 0, 100, 0));
  
  // &:before,
  // &:after
  // {
  //   position: absolute;
  //   content:" ";
  //   top:0;
  //   left:0;
  //   right:0;
  //   bottom:0;
  //   background: linear-gradient(0deg, rgba(0, 0, 200, 0.4), rgba(0, 0, 200, 0));
  // }
  
  // &:after
  // {
  //   background: linear-gradient(240deg, rgba(150, 50, 50, 0.4), rgba(0, 0, 200, 0));
  // }
}

.info
{
  font-family: 'Oxygen', sans-serif;
  color: white;
  position: absolute;
  bottom: 10px;
  left: 10px;
}
</style>
