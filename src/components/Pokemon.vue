<template>
    <div>
        <p v-text="Pokemon.name"></p>
        <div>
            <select v-model="poke" v-html="list" v-on:change="changePokemon"></select>
        </div>
        <div><button v-text="moveBtnMsg" v-on:click="showMoves"></button></div>
        <div><button v-text="typeBtnMsg" v-on:click="showTypes"></button></div>
        <div>
            <div v-html="typeTable"></div>
        </div>
        <div>
            <div v-html="moveTable"></div>
        </div>
    </div>
</template>

<script>
import List from './pokemon/List.vue'

import PikachuObj from './pokemon/Pikachu.vue'
import EeveeObj   from './pokemon/Eevee.vue'
import MewtwoObj  from './pokemon/Mewtwo.vue'
import MewObj     from './pokemon/Mew.vue'

let PokemonObj = {
    name : 'Pokemon',
    data : function() {
        return {
            Pokemon : PikachuObj,
            moveBtnMsg  : '技を表示',
            moveTable : '',
            typeBtnMsg : 'タイプを表示',
            typeTable : '',
            poke : 'pikachu',
        }
    },
    computed: {
        list : function() {
            let PokemonList = List.PokemonList
            let tag = '';
            for (let i in PokemonList) {
                tag += `<option value="${i}">${PokemonList[i]}</option>`;
            }
            return tag;
        }
    },
    methods : {
        changePokemon : function() {
            if (this.poke === 'pikachu') {
                this.Pokemon = PikachuObj;
            } else if (this.poke === 'eevee') {
                this.Pokemon = EeveeObj;
            } else if (this.poke === 'mewtwo') {
                this.Pokemon = MewtwoObj;
            } else if (this.poke === 'mew') {
                this.Pokemon = MewObj;
            }

            if (this.moveBtnMsg === '技を非表示') {
                this.moveBtnMsg = '技を表示';
            } else {
                this.moveBtnMsg = '技を非表示';
            }
            this.showMoves();

            if (this.typeBtnMsg === 'タイプを非表示') {
                this.typeBtnMsg = 'タイプを表示';
            } else {
                this.typeBtnMsg = 'タイプを非表示';
            }
            this.showTypes();
        },
        showMoves : function() {
            if (this.moveBtnMsg === '技を非表示') {
                this.moveBtnMsg = '技を表示';
                this.moveTable = '';
                return;
            }

            this.moveBtnMsg = '技を非表示';
            let tableHeader = '<tr><th>レベル</th><th>覚える技</th></tr>';

            let initMovesTr = '';
            for (let i in this.Pokemon.initMoves) {
                initMovesTr += `<tr><td>基本</td><td>${this.Pokemon.initMoves[i]}</td></tr>`;
            }

            let levelUpMovesTr = '';
            for (let i in this.Pokemon.levelUpMoves) {
                levelUpMovesTr += `<tr><td>レベル${i}</td><td>${this.Pokemon.levelUpMoves[i]}</td></tr>`;
            }

            this.moveTable = '<table >' + tableHeader + initMovesTr + levelUpMovesTr + '</table>';
        },
        showTypes : function() {
            if (this.typeBtnMsg === 'タイプを非表示') {
                this.typeBtnMsg = 'タイプを表示';
                this.typeTable = '';
                return;
            }

            this.typeBtnMsg = 'タイプを非表示';

            let typeTr = '';
            for (let i in this.Pokemon.type) {
                typeTr += `<tr><td>タイプ${i}</td><td>${this.Pokemon.type[i]}</td></tr>`;
            }

            this.typeTable = '<table >' + typeTr + '</table>';
        }
    }
}

export default PokemonObj
</script>