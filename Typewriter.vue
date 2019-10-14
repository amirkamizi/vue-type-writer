<template>
    <div class="card">
        <div class="card-header">
            Typewriter
        </div>

        <div class="card-body">
            {{shownText}}{{blinkingcurser}}
        </div>
    </div>
</template>

<script>
    export default {
        // props: ['texts'],
        data: function(){
            return {
                index : 0,
                textIndex : 0,
                text : ['Hello Lurem ipsum','another text is here'],
                shownText:'',
                speed:100, // in milliseconds
                curser: '|',
                blinkingcurser : '',
                curserBlinkingSpeed:400, //in milliseconds
                erase: false,
                waiter : 0,
                defaultwaiter:50, //50 times of speed. 50 * 100
            }
        },
        computed:{
        },
        methods:{
            typeIt : function(){
                if(this.textIndex<this.text.length){
                    if(this.text[this.textIndex].length > 0 && this.shownText != this.text[this.textIndex] && !this.erase){
                        this.waiter = this.defaultwaiter;
                        this.shownText = this.text[this.textIndex].substr(0,this.index);
                        this.index++;
                    }else if(this.shownText.length == 0){
                        this.erase = false;
                        this.textIndex++;
                    }else if(this.shownText == this.text[this.textIndex] || this.erase){
                        if(this.waiter == 0){
                            this.erase = true;
                            this.shownText = this.text[this.textIndex].substr(0,this.index);
                            this.index--;
                        }else{
                            this.waiter--;
                        }
                    }
                }else{
                    this.textIndex = 0;
                }
            },
            blinking : function(){
                // this.shownText = "you" + this.blinkingcurser;
                if(this.blinkingcurser != ''){
                    this.blinkingcurser = '';
                }else{
                    this.blinkingcurser = this.curser;
                }
            }
        },
        created(){
            setInterval(this.typeIt,this.speed)
            setInterval(this.blinking,this.curserBlinkingSpeed)
        }

    }
</script>
