<template>
    <div id="app">
        <header class="title">井字棋（错）</header>
        <main class="content">
            <table>
                <thead>
                    <tr>
                        <th colspan="3">规则</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in gokoList" :key="index">
                        <td v-for="(small, num) in gokoList[index]" :key="num">
                            <Cell
                                @click="onClickCell((num + index * 3), $event, gokoList[index])"
                                :childN="parentN" />
                        </td>
                    </tr>
                </tbody>
            </table>
        </main>
    </div>
</template>

<script>
import Cell from './components/cell.vue'

export default {
    components: {
        Cell
    },
    data(){
        return {
            parentN: 0,
            shut: false,
            gokoList: [
                [null, null, null],
                [null, null, null],
                [null, null, null]
            ],
            result: 'x先手'
        }
    },
    methods: {
        onClickCell(index, text) {
            this.gokoList[Math.floor(index / 3)][index % 3] = text
            this.parentN += 1
            if(this.shut) {
                return 
            }
            if(text === 'x'){
                this.result = '轮到o了'
            }else if(text === 'o'){
                this.result = '轮到x了'
            }
        }
    }
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    .title {
        text-align: center;
        padding: 20px 10px;
    }
    .content {
        display: flex;
        justify-content: center;
        table {
            border-collapse: collapse;
            td {
                border: 6px solid #ccc;
                width: 100px;
                height: 100px;
            }
        }
    }
}
</style>
