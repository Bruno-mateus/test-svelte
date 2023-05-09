<script lang="ts">
  import axios from 'axios'
  let isLoading:boolean
  let imgURL:string
  async function getCat(){
    try{
      isLoading = true
      const response = await axios.get("https://cataas.com/cat?json=true")
      imgURL = `https://cataas.com/${response.data.url}`
    }catch(err){
      alert(err)
    }finally{
      isLoading=false
    }
  }

function handleCat(){  
  getCat()
}
</script>




<div class="banner">
  {#if isLoading}
  <div class="LoadingIndicator">
    <strong>
      Loading
    </strong>
  </div>
  {/if}
  <img src={imgURL} alt="">
</div>

<button on:click={()=>handleCat()}>
  Random cat
</button>
 
<style>
  .banner{
    width:320px;
    height: 280px;
    position: relative;
  }
  img{
    width: 100%;
    height: 100%;
    object-fit: cover;
  }


  .LoadingIndicator {
    display: flex;
    background: rgba(0,0,0,0.2);
    justify-content: center;
    align-items: center;
    text-align: center;
    position: absolute; 
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    z-index: 20;
    font-size: 40px;
    color:white
}

</style>