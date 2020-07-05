<template>
    <div class="artist">
        <div :class="'artist-inner ' + artist.color">
            <div class="artist-text-wrap">
                <h2 class="bg-text">
                    {{ artist.bgtext }}
                </h2> 
            </div>
            <div class="artist-image-wrap">
                <img :src="artist.src" class="image"/>
            </div>
            <div class="artist-detail">
                <h2> {{ artist.title }} </h2>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Optio, aliquam.</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'artist',
    props: ['artist'],
}
</script>

<style>
  .artist {
    flex: 1 1 33.333%;
    width: 100%;
    padding: 25px;
  }
  .artist-inner {
    position: relative;
    padding: 25px;
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    perspective: 1000px;
  }
  .artist-inner.green {
    background-image: linear-gradient(to bottom right, #24D484, #116432);
  }
  .artist-inner.blue {
    background-image: linear-gradient(to bottom left, #24D484, #2474C4 70%);
  }
  .artist-inner.pink {
    background-image: linear-gradient(to bottom right, #F444A4, #1168D4);
  }
  .artist-text-wrap {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 0;
    overflow: hidden;
    perspective: 1000px;
  }
  
  .artist-text-wrap h2 {
    color: #313131;
    font-size: 128px;
    font-weight: 900;
    opacity: 0.2;
    transform-origin: center;
  }
  .artist-image-wrap {
    position: relative;
    z-index: 1;
    transform-origin: center;
  }
  .artist-image-wrap .image {
    width: 100%;
    filter: drop-shadow(0px 0px 12px rgba(0, 0, 0, 0.25));
  }
  .artist-detail {
    background-color: #FFF;
    padding: 25px;
    margin: 0px -25px -25px;
  }
  .artist-detail h2 {
    font-size: 24px;
    font-weight: 700;
    color: #676767;
    margin-bottom: 15px;
  }
  .artist-detail p {
    font-size: 14px;
    line-height: 1.5;
    font-weight: 300;
    color: #676767;
  }
</style>