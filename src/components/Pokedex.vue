<template>
    <div>
        <p v-text="Pokemon.name"></p>
        <div>
            <select v-model="poke" v-html="list"></select>
        </div>
        <div><button v-text="typeBtnMsg" v-on:click="showTypes"></button></div>
        <div><button v-text="moveBtnMsg" v-on:click="showMoves"></button></div>
        <div>
            <div v-if="showType" v-html="typeTable"></div>
        </div>
        <div>
            <div v-if="showMove" v-html="moveTable"></div>
        </div>
    </div>
</template>

<script>
import Pokemon from './pokedex/pokemon.vue'

let PokemonObj = {
    name : 'Pokemon',
    data : function() {
        return {
            showMove : false,
            showType : true,
            poke : 25,
            pokemonList : Pokemon.Pokemon,
        }
    },
    computed: {
        list : function() {
            let tag = '';
            for (let i in this.pokemonList) {
                tag += `<option value="${i}">${this.pokemonList[i].name}</option>`;
            }
            return tag;
        },
        Pokemon : function() {
            return Pokemon.Pokemon[this.poke]
        },
        typeBtnMsg : function() {
            let msg = 'タイプを表示';
            if (this.showType) {
                msg = 'タイプを非表示';
            }
            return msg;
        },
        typeTable : function() {
            let typeTr = '';
            for (let i in this.Pokemon.type) {
                typeTr += `<tr><td>タイプ${i}</td><td>${this.Pokemon.type[i]}</td></tr>`;
            }

            return '<table >' + typeTr + '</table>';
        },
        moveBtnMsg : function() {
            let msg = '技を表示';
            if (this.showMove) {
                msg = '技を非表示';
            }
            return msg;
        },
        moveTable : function() {
            let tableHeader = '<tr><th>レベル</th><th>覚える技</th></tr>';

            let initMovesTr = '';
            for (let i in this.Pokemon.initMoves) {
                initMovesTr += `<tr><td>基本</td><td>${this.Pokemon.initMoves[i]}</td></tr>`;
            }

            let levelUpMovesTr = '';
            for (let i in this.Pokemon.levelUpMoves) {
                levelUpMovesTr += `<tr><td>レベル${i}</td><td>${this.Pokemon.levelUpMoves[i]}</td></tr>`;
            }

            return '<table >' + tableHeader + initMovesTr + levelUpMovesTr + '</table>';
        },
    },
    methods : {
        showTypes : function() {
            this.showType = !this.showType;
        },
        showMoves : function() {
            this.showMove = !this.showMove;
        },
    }
}

export default PokemonObj
</script>