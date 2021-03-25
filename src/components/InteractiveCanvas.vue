<template>
    <div>
        <canvas id="myCanvas" width="1000" height="500" @mousedown="beginDrawing" @mouseup="stopDrawing" @mousemove="pan"/> <!--@-->
        <div class="q-pa-md">
            <div class="row justify-center">
                <div class="col">
                    <q-btn color="white" text-color="black" label="Undo" @click="undo"/>
                </div>
                <div class="col-6">
                    <q-color v-model="hex" no-footer default-view="palette"
                    :palette=this.colors
                    class="my-picker" />
                </div>
                <div class="col">
                    <q-btn color="primary" label="Submit" />
                </div>
            </div>
        </div>
        <span>Pixels remaining: {{count}}</span>
        <ul>
            <li v-for="(pixel, index) in pixels" :key="index">{{pixel}}</li>
        </ul>
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
            count: 20,

            hex: '#fff100',

            pixels: [],
            colors: ['#fff100', '#ff8c00', '#e81123', '#ec008c','#68217a', '#00188f','#00bcf2','#00b294','#009e49','#bad80a']
        }
    },
    methods: {
        beginDrawing(e) {
            this.x = e.offsetX;
            this.y = e.offsetY;
            this.isDrawing = true;
        },

        checkColor(hex){
            return (this.colors.indexOf(hex));
        },
        
        calcPost(x,y){
            return (y*1000)+x;
        },

        undo(){
            let p = this.pixels.pop().pos
            let ctx = this.canvas;
            ctx.fillStyle = 'white';
            ctx.fillRect( p.x-5, p.y-5, 5, 5);
            this.count++;
        },

        stopDrawing(e) {
            if (this.isDrawing === true && this.count > 0) {
                var rectSize = 5;
                let ctx = this.canvas;
                ctx.fillStyle = this.hex;
                ctx.fillRect( this.x-rectSize, this.y-rectSize, rectSize, rectSize);

                this.pixels.push({color:this.checkColor(this.hex),pos:{x:this.x,y:this.y}});
                this.x = 0;
                this.y = 0;
                this.count --;
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
}
</style>