<template>
    <div id="carousel">
        <div id="banner" v-if="images">
            <div v-for="n in 4" :key="n" class="panel">
                <img :src="n == 1 ? images[2].src : images[n-2].src"/>
            </div>
        </div>

        <div id="banner-top" v-if="images">
            <div  v-for="n in 3" :key="n" class="panel" :style='n == 2 ? "transform: scale(1)" : "transform: scale(.9)"'>
                <img :src="images[n-1].src"/>
            </div>
        </div>

        <!--<div id="overlay" :style="hover ? 'opacity: .3' : 'opacity: 0'"></div>
        <div id="button"><h3 @mouseover="hover = true" @mouseleave="hover = false">Starting at<br>$139.99</h3></div>-->
    </div>
</template>

<script>
export default {
    name : 'Carousel',
    data() {
        return {
            images : [
                {
                id : 0,
                src: require('../assets/images/product/one.jpg')
                },
                {
                id : 1,
                src: require('../assets/images/product/two.jpg')
                },
                {
                id : 2,
                src: require('../assets/images/product/three.jpg')
                }
            ],
            timimg : null,
            refreshScrollableArea : null,
            hover: false,
        }
    },
    methods : {
        buttonHover() {
            console.log('gover!');
        },
        sizeChange() {
            console.log('size change');
        },
        createTimer() {
            this.timimg = setInterval(async () => {
        
                document.getElementById("banner-top").style.opacity = "0";
                document.getElementById("banner").style.opacity = "1";
                document.getElementById("banner").style.transform = "translate(25%)";

                let panels = document.querySelectorAll('#banner > .panel');
                //console.log(panels[1]);

                panels[1].style.transform = "scale(1)";
                panels[2].style.transform = "scale(.9)";

                let temp = this.images[2];
                this.images[2] = this.images[1];
                this.images[1] = this.images[0];
                this.images[0] = temp;
                
                await new Promise(resolve => setTimeout(resolve, 2000));

                

                this.$forceUpdate();

                document.getElementById("banner").style.opacity = "0";
                document.getElementById("banner-top").style.opacity = "1";

                panels[2].style.transform = "scale(1)";
                panels[1].style.transform = "scale(.9)";
                
                document.getElementById("banner").style.transform = "translate(0px)";
            }, 5000);
        }
    },
    beforeDestroy() {
        console.log('killing!');
        clearInterval(this.timimg);
        clearInterval(this.refreshScrollableArea);
    },
    mounted() {

        // update height of carousel
        this.refreshScrollableArea = setInterval(() => {
            const { offsetHeight } = document.getElementById('banner');
            document.getElementById('carousel').style.height = `${offsetHeight}px`;
        }, 100);
        
        let panels = document.querySelectorAll('#banner > .panel');
        panels[2].style.transform = "scale(1)";

        this.$forceUpdate();
        this.createTimer();
    }
}
</script>

<style scoped>

#button {
    position: absolute;
    z-index: 999;
    left: 50%;
    color: white;
    font-size: 100%;
}

h3 {
    position: relative;
    margin-top: 150%;
    left: -50%;
    border: 3px white solid;
    padding: 15px;
    transition: background-color .5s;
    font-size: 1.5em;
}

h3:hover {
    cursor: pointer;
    background: rgba(255, 255, 255,.2);
}

#carousel {
    position: relative;
    width: 100%;
    background: rgb(53, 53, 53);
    padding-top: 20px;
    padding-bottom: 20px;
}

#carousel::after {
    pointer-events: none;
    background: linear-gradient(90deg, rgba(0, 0, 0,.7) 5%, rgba(255,255,255,0) 25%, rgba(255,255,255,0) 75%, rgba(0, 0, 0,.7) 95%);
    content: "";
    position: absolute;
    left: 0;
    z-index: 997;
    height: inherit;
    top: 0;
    width: 100%;
    opacity: .3;
    padding-top: 20px;
    padding-bottom: 20px;
  }

#banner, #banner-top {
    display: inline-flex;
    position: absolute;
    left: 50%;
}

#banner {
  width: 240%;  
  margin-left: calc(-120% - 30%);
  transition: transform 2s;
  opacity: 1;
}

#banner-top {
  width: 180%;
  margin-left: -90%;
  opacity: 0;
}

.panel {
  display: inline;
  transition: transform 2s;
  transform: scale(.9);
}

#banner-top img, #banner img  {
  width: 100%;
  border-radius: 10px;
}

#overlay {
    top: 0;
    position: absolute;
    background: black;
    backdrop-filter: blur(100px);
    width: 100%;
    height: inherit;
    z-index: 998;
    transition: opacity .55s;
    padding-top: 20px;
    padding-bottom: 20px;
}

</style>