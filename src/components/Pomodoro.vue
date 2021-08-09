<template>
    <div class="app-pomodoro">
        <div class="pomodoro"> 
            <div class="title"> Pomodoro </div>
            <div class="chronometer"> 
                <div class="cycle"> Time to {{ cycle }} ! </div>
                <div class="clock">
                    {{displayMinutes}} : {{displaySeconds}} 
                </div>
                <div class="button">
                    <div class="start" v-on:click="start()"> 
                        {{status}}  
                    </div>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>
    
    export default {
        name: 'Pomodoro',
        data: () => ({
            displayMinutes: '00',
            displaySeconds: '00',
            minutes:  0,
            seconds: 0,
            started: false,
            status: "START",
            numberBlock: 0,
            cycle: "work"
        }),
        props:{
            minutesPause: Number,
            minutesLongPause: Number,
            minutesWork: Number,
            numberOfBlocks: Number
        },
        mounted(){
            this.setNumberBlocks(this.numberOfBlocks),
            this.setMinutes(this.minutesWork),
            this.startCountDown()
        },
        methods: {
            changeColorStarted(){
                document.getElementsByClassName("pomodoro")[0].style.background = (this.cycle == "work")?"#ff6b6b":"#7bed9f";
                document.body.style.background = (this.cycle=="work")?'#ee5253':"#2ed573";
            },
            changeColorPaused(){
                document.getElementsByClassName("pomodoro")[0].style.background = '#7f8fa6';
                document.body.style.background = '#2f3640';
            },
            setNumberBlocks(nb){
                this.numberBlock = nb;
            },
            setMinutes(minutes){
                this.minutes = minutes;
                if(minutes < 10) this.displayMinutes = '0'+minutes.toString();
                else this.displayMinutes = minutes.toString();
            },
            start(){
                this.started = !(this.started);
                if(this.started){
                    this.status = "PAUSE";
                    this.changeColorStarted();
                }else{
                    this.status = "START";
                    this.changeColorPaused();
                }
                    
            },
            startCountDown(){
                setInterval( () =>{

                    if(this.seconds == 0 && this.minutes == 0){
                        window.alert('Block finishedd!');
                        if(this.cycle == "work"){
                            this.cycle = "break";
                            this.setMinutes(this.minutesPause);
                            
                        }else{
                            
                            this.numberBlock = this.numberBlock - 1;

                            if(this.numberBlock == 0){
                                this.cycle = "a long break";
                                this.setMinutes(this.minutesLongPause);
                            }else{
                                this.cycle = "work";
                                this.setMinutes(this.minutesWork);
                                if(this.numberBlock < 0) this.numberBlock = this.numberOfBlocks;
                            }
                            
                        }
                        this.changeColorStarted();
                    }else{
                        if(this.started){   
                        
                            if (this.seconds == 0){
                                this.seconds = 59;
                                this.minutes = this.minutes - 1;
                            }else
                                this.seconds = this.seconds - 1;
                            
                            if(this.minutes < 10) this.displayMinutes = '0' + this.minutes.toString();
                            else this.displayMinutes = this.minutes.toString();

                            if(this.seconds < 10 ) this.displaySeconds = '0' + this.seconds.toString();
                            else this.displaySeconds = this.seconds.toString();

                        }
                    }
                }, 1000);
                
            }
        }
    };
</script>

<style scoped>

    .pomodoro{
        text-align: center;
        width: 40%;
        margin-left: 30%;
        background-color: #7f8fa6/*#ff6b6b*/;
        color: white;
        border-radius: 20px;
    }

    .title{
        font-family: Avenir, Helvetica, Arial, sans-serif;
        font-size: 25px;
        margin-top: 50px;
        margin-bottom: 25px;
    }

    .cycle{
        font-family: Avenir, Helvetica, Arial, sans-serif;
        font-size: 50px;
        margin-bottom: 5px;
    }

    .clock{
        font-family: Avenir, Helvetica, Arial, sans-serif;
        font-size: 100px;
        margin-bottom: 15px;
    }

    .button{
        text-align: center;
    }

    .start{
        width: 25%;
        font-size: 25px;
        border-width: 1px;
        border-style: solid;
        border-color: white;
        border-radius: 10px;
        margin-left: 35%;
        padding: 20px;
        cursor: pointer;
        font-family: Avenir, Helvetica, Arial, sans-serif;
        background-color: transparent;
    }

    
</style>
