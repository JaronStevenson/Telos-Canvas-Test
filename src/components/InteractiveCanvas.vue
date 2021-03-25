<template>
    <div>
        <canvas id="myCanvas" width="1000" height="500" @mousedown="beginDrawing" @mouseup="stopDrawing" @mousemove="pan"/> <!--@-->
        <q-color v-model="hex" no-footer default-view="palette"
            :palette=
                "['#fff100', '#ff8c00', '#e81123', '#ec008c','#68217a', '#00188f','#00bcf2','#00b294','#009e49','#bad80a']" 
            class="my-picker" />
    </div>
</template>

<script>
export default {
    props: ({
        color: String
    }),
    data() {
        return {
            x: 0,
            y: 0,
            isDrawing: false,
            canvas: null,

            hex: '#FF00FF'
        }
    },
    methods: {
        beginDrawing(e) {
            this.x = e.offsetX;
            this.y = e.offsetY;
            this.isDrawing = true;
        },

        stopDrawing(e) {
            if (this.isDrawing === true) {
                var rectSize = 5;
                let ctx = this.canvas;
                ctx.fillStyle = this.hex;
                ctx.fillRect( this.x-rectSize, this.y-rectSize, rectSize, rectSize);

                this.x = 0;
                this.y = 0;
                this.isDrawing = false;
                
            }
        },
        
        pan(e){
            this.isDrawing =false;
        }
    },
    mounted(){
      var c = document.getElementById("myCanvas");
      this.canvas = c.getContext('2d');
    }
}
</script>


<style>
#myCanvas {
    border: 1px solid grey;
    zoom: 500%;
}
</style>