<template>
    <div class="hang-post">
        <div class="head" v-if="wrongAnswers > 0"></div>
        <div class="body" v-if="wrongAnswers > 1"></div>
        <div class="left-arm" v-if="wrongAnswers > 2"></div>
        <div class="right-arm" v-if="wrongAnswers > 3"></div>
        <div class="left-leg" v-if="wrongAnswers > 4"></div>
        <div class="right-leg" v-if="wrongAnswers > 5"></div>
    </div>
</template>

<script>
export default {
    props: [
        'wrongAnswers'
    ]
}
</script>

<style>
    .hang-post {
        position: relative;
        border-top: solid black 2px;
        border-left: solid black 2px;
        width: 100px;
        height: 300px;
    }

    .hang-post::before {
        position: absolute;
        content: "";
        width: 2px;
        background-color: black;
        height: 30px;
        top: 0px;
        left: 96px;
    }

    .hang-post::after {
        position: absolute;
        content: "";
        height: 2px;
        width: 80px;
        bottom: 0px;
        background-color: black;
        left: -40px;
    }

    .head {
        position: absolute;
        width: 50px;
        height: 50px;
        border: solid red 2px;
        border-radius: 50px;
        top: 30px;
        left: 73px;
    }

    .body {
        position: absolute;
        width: 2px;
        height: 100px;
        background-color: red;
        left: 96px;
        top: 80px;
    }

    .left-arm {
        position: absolute;
        width: 2px;
        height: 40px;
        background-color: red;
        transform: rotate(-60deg);
        top: 85px;
        left: 78px;
    }

    .right-arm {
        position: absolute;
        width: 2px;
        height: 40px;
        background-color: red;
        transform: rotate(60deg);
        top: 85px;
        left: 114px;
    }

    .left-leg {
        position: absolute;
        width: 2px;
        height: 60px;
        background-color: red;
        transform: rotate(35deg);
        top: 174px;
        left: 78px;
    }

    .right-leg {
        position: absolute;
        width: 2px;
        height: 60px;
        background-color: red;
        transform: rotate(-35deg);
        top: 174px;
        left: 114px;
    }
</style>
