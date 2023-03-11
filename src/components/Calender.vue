<template>
    <main>
        <div class="container">
            <div class="col-6 left">
                <h3>{{ days[currentDay] }}</h3>
                <h1>{{ currentDate }}</h1>
            </div>
            <div class="col-6 right">
                <h3>{{ currentMonthName }} {{ currentYear }}</h3>
                <div class="days">
                    <span v-for="(day, index) in days" :key="index">{{ day }}</span>
                </div>
                <div class="dates">
                    <span v-for="day in firstDay" :key="day"></span>
                    <span :class="todayDate(date)" v-for="(date, index) in lastDateOfMonth" :key="index">{{ date }}</span>
                </div>
                <div class="btn-group">
                    <button @click="prev()">Prev</button>
                    <button @click="next()">Next</button>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
    export default {
        data(){
            return{
                days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
                // months: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
                // currentMonth: new Date().getMonth(),
                currentDate: new Date().getDate(),
                currentDay: new Date().getDay(),

                currentMonthInNumber: new Date().getMonth(),
                currentYear: new Date().getFullYear(),
            }
        },
        computed:{
            currentMonthName(){
                return new Date(this.currentYear,this.currentMonthInNumber).toLocaleString("default", {month:"long"})
            },
            lastDateOfMonth(){
                return new Date(this.currentYear, this.currentMonthInNumber+1,0).getDate()
            },
            firstDay(){
                return new Date(this.currentYear, this.currentMonthInNumber).getDay()
            }
        },
        methods:{
            next(){
                if(this.currentMonthInNumber===11){
                    this.currentYear++
                    this.currentMonthInNumber=0
                }else{
                    this.currentMonthInNumber++
                }
            },
            prev(){
                if(this.currentMonthInNumber===0){
                    this.currentYear--
                    this.currentMonthInNumber=11
                }else{
                    this.currentMonthInNumber--
                }
            },
            todayDate(date){
                let calenderDate = new Date(this.currentYear, this.currentMonthInNumber, date).toDateString()
                let toDay = new Date().toDateString()
                return calenderDate === toDay ? "active" : ""
            }
        }
    }
</script>

<style>
    main{
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100vh;
    }
    .container{
        width: 1000px;
        margin: 0 auto;
        height: auto;
        background: #43dde6;
        display: flex;
        border-radius: 10px;
        height: 400px;
    }
    .col-6{
        width: 50%;
    }
    .col-6:last-child{
        background: #fff;
        border-radius: 0 10px 10px 0;
    }
    .right h3{
        text-align: center;
        font-weight: bolder;
        color: #43dde6;
        font-size: 26px;
    }
    .right .dates{
        min-height: 230px;
    }
    .right .dates,
    .right .days{
        display: flex;
        flex-wrap: wrap;
        flex-grow: 1;
    }
    .right .dates span,
    .right .days span{
        flex-basis: 14.28%;
        text-align: center;
        color: #fc85ae;
        font-weight: bold;
    }
    .right .dates span{
        color: #000 !important;
        margin-top: 15px;
    }
    .right .btn-group{
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 20px 15px;
    }
    .right .btn-group button{
        border: none;
        background: #43dde6;
        font-weight: bold;
        font-size: 14px;
        color: #fff;
        padding: 5px 15px;
        border-radius: 3px;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    .right .btn-group button:active{
        background: #03969e;
    }
    .right span.active{
        color: red !important;
    }




    .left h3{
        font-size: 26px;
        text-transform: uppercase;
        text-align: center;
        color: #b1fbff;
    }
    .left h1{
        font-size: 200px;
        text-align: center;
        margin: 0;
        color: #fff;
    }
    
</style>