<script setup>
//------import zone--------

import { ref } from 'vue';
//--------variabele zone------
const fild = ref([]);
const wFild = 50;
const hFild = 50;
const snake = [];
let xStart = 23;
let yStart = 25;
let isStartGame = false
//----------function zone----------
function startGame() {
    if (!isStartGame) {
        generetedFild(wFild, hFild)
        generetedSnake(xStart, yStart)
        insertSnakeToFild()
    }
    isStartGame = true
}
function generetedFild(w, h) {
    for (let x = 0; x < w; x++) {
        for (let y = 0; y < h; y++) {
            fild.value.push(
                {
                    x: x,
                    y: y,
                    text: "",
                    snake: false
                }
            )
        }

    }
}
function generetedSnake(x, y) {
    for (let i = 0; i < 3; i++) {
        if (i == 0) {
            snake.push(
                {
                    x: x,
                    y: y,
                    body: "tail"
                }
            )

        }
        else if (i == 2) {
            snake.push(
                {
                    x: x,
                    y: y,
                    body: "head"
                }
            )
        } else {
            snake.push(
                {
                    x: x,
                    y: y,
                    body: "body n°1"
                }
            )
        }
        console.log(x);
        y++
    }
}
function insertSnakeToFild() {
    fild.value.forEach(pixel => {
        snake.forEach(bodySnake => {
            if (pixel.x === bodySnake.x && pixel.y === bodySnake.y) {
                pixel.snake = true;
                pixel.text = bodySnake.body
            }
        })
    })
}
</script>

<template>
    <a class="btn btn-primary" @click="startGame()" v-show="!isStartGame">Start Game</a>
    <div class="fild border border-5" v-show="isStartGame" >
        <div v-for="pixel in fild" class="pixel border border-1 d-inline-block p-1"
            :class="(pixel.snake ? 'bodySnake' : ''), (pixel.text === 'tail' ? 'tail' : ''), (pixel.text === 'head' ? 'head' : '')"
            >
        </div>
    </div>
</template>

<style scoped>
.fild {
    height: 100vh;
    line-height: 0;
}

.pixel {
    width: calc(100%/50);
    height: calc(100%/50);
}

.head {
    background-color: green;
}

.bodySnake {
    background-color: greenyellow;
}

.tail {
    background-color: rgb(195, 248, 149);
}
</style>
