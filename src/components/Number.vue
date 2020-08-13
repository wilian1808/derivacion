<template>
    <div class="number">
        <div class="number__content">

            <!-- <form class="form" @submit.prevent="getData">
                <input class="form__text" v-model="url" type="text" name="" id="">
                <input @click="getData" class="form__button" type="submit" value="consultar">
            </form> -->

            <table class="tabla">
                <tr class="tabla__tr">
                    <th class="tabla__th">tiempo</th>
                    <th class="tabla__th">2</th>
                    <th class="tabla__th">3</th>
                    <th class="tabla__th">4</th>
                    <th class="tabla__th">5</th>
                    <th class="tabla__th">6</th>
                    <th class="tabla__th">7</th>
                </tr>

                <tr class="tabla__tr">
                    <td class="tabla__td">velocidad</td>
                    <td class="tabla__td">6.010</td>
                    <td class="tabla__td">8.144</td>
                    <td class="tabla__td">12.022</td>
                    <td class="tabla__td">14.990</td>
                    <td class="tabla__td">16.781</td>
                    <td class="tabla__td">20.451</td>
                </tr>
            </table>

            <div class="valores">
                <label class="valores__label">
                    <span class="valores__span">h</span>
                    <input class="valores__text" v-model="h" type="text" name="" id="">
                </label>

                <label class="valores__label">
                    <span class="valores__span">X0</span>
                    <input class="valores__text" v-model="x0" type="text" name="" id="">
                </label>
            </div>

            <div class="opciones">
                <button class="opciones__button" @click="progresiva">Progresiva</button>
                <button class="opciones__button" @click="regresiva">Regresiva</button>
                <button class="opciones__button" @click="central">Centrada</button>
            </div>

            <div class="resultado" style="grid-template-columns: repeat(3, 1fr)">
                <div v-show="progre" class="resultado__pro">
                    <h4>diferencias finitas progresivas</h4>
                    <p>con dos puntos: {{ proDosPuntos.toFixed(3) }}</p>
                    <p>con tres puntos: {{ proTresPuntos.toFixed(3) }}</p>
                </div>

                <div v-show="regre" class="resultado__reg">
                    <h4>diferencias finitas regresivas</h4>
                    <p>con dos puntos: {{ regDosPuntos.toFixed(3) }}</p>
                    <p>con tres puntos: {{ regTresPuntos.toFixed(3) }}</p>
                </div>

                <div v-show="centra" class="resultado__cen">
                    <h4>diferencias finitas centrales</h4>
                    <p>con dos puntos: {{ cenDosPuntos.toFixed(3) }}</p>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
import Drive from 'drive-db'

export default {
    name: 'Number',
    data() {
        return {
            url: '1tr59FkHCvndjqxrTYsAJPmNhEa279fldLdjfg0XJP-M',
            datos: [],
            h: 1,
            x0: 4,
            valores: [0, 0, 6.010, 8.144, 12.022, 14.990, 16.781, 20.451],
            proDosPuntos: 0,
            proTresPuntos: 0,
            regDosPuntos: 0,
            regTresPuntos: 0,
            progre: false,
            regre: false,
            centra: false,
            cenDosPuntos: 0,
            contador: 0
        }
    },
    methods: {
        async getData() {
            let response = await Drive(`${this.url}`)
            this.datos = response
        },

        progresiva() {
            // let h = 1, X0 = 2;
            let h = parseInt(this.h)
            let X0 = parseInt(this.x0)
            // con 2 puntos
            // f(X0) = ( f(X0 + h) - f(X0) ) / h
            this.proDosPuntos = (  this.valores[X0 + h] - this.valores[X0]) / h;
            // f(X0) = ( -3f(X0) + 4f(X0 + h) - f(X0 + 2h) / 2h )
            this.proTresPuntos = ( (-3 * this.valores[X0]) + (4 * this.valores[X0 + h]) - this.valores[X0 + (2 * h)] ) / (2 * h);
            
            if (!this.progre) {
                this.contador++
                this.progre = true
            }  else {
                this.contador--
                this.progre = false
            }
        },

        regresiva() {
            // let h = 1, X0 = 4;
            const h = parseInt(this.h);
            const X0 = parseInt(this.x0);

            // con 2 puntos
            // f(X0) = (f(X0) - f(X0 - h)) / h
            this.regDosPuntos = ( this.valores[X0] - this.valores[X0 - h] ) / h;

            // con 3 puntos
            // f(X0) = (f(X0 - 2h) - 4f(X0 - h) + 3(X0)) / 2h
            this.regTresPuntos = ( this.valores[X0 - (2*h)] - (4 * this.valores[X0 - h]) + (3 * this.valores[X0])) / (2 * h);
            
            if (!this.regre) {
                this.contador++
                this.regre = true
            } else {
                this.contador--
                this.regre = false
            }
        },

        central() {
            // let h = 1, X0 = 4
            const h = parseInt(this.h);
            const X0 = parseInt(this.x0);

            // con 2 puntos
            // f(X0) = (f(X0 + h) - f(X0 - h)) / 2h
            this.cenDosPuntos = ( this.valores[X0 + h] - this.valores[X0 - h] ) / (2 * h);

            // con 4 puntos
            // f(X0) = (f(X0 - 2h) - 8f(X0 - h) + 8f(X0 + h) - f(X0 + 2h)) / 2h
            // resultado = 3.66641
            // const resultadoTresPuntos = ( valores[X0-(2*h)] - (8*valores[X0-h]) + (8*valores[X0+h]) - valores[X0+(2*h)] ) / (2*h);

            if (!this.centra) {
                this.contador++
                this.centra = true
            } else {
                this.contador--
                this.centra = false
            }
        }
    },
    
    created() {
        //this.getData();
    },
}
</script>

<style scoped>
.number {
    display: block;
    width: 100%;
    background-color: #18191a;
}

.number__content {
    width: 92%;
    margin: 0 auto 0;
}

.form {
    display: grid;
    grid-template-columns: 380px 90px;
    justify-content: center;
    grid-gap: 1em;
    padding: 1em 0;
}

.form__text,
.form__button {
    font-size: 14px;
    padding: .8em 0;
    border: none;
    border: solid 1.5px #eeeeee;
    text-align: center;
    border-radius: 3px;
}

.form__text {
    padding: 0 1em;
}

.form__button {
    cursor: pointer;
    border-color: #eeeeee;
    background-color: transparent;
    color: #eeeeee;
}

.form__button:hover {
    background-color: #eeeeee;
    color: #18191a;
}

.form__button:active {
    transform: scale(.96);
}

.tabla {
    margin: 1em auto 0;
    text-align: center;
}

.tabla__th,
.tabla__td {
    display: inline-block;
    border: solid 1px #eeeeee;
    width: 80px;
    padding: .5em 0;
    color: #eeeeee;
}

.valores {
    margin: 1em auto 0;
    display: grid;
    grid-template-columns: 150px 150px;
    justify-content: center;
    grid-gap: 1em;
}

.valores__label {
    display: grid;
    grid-template-columns: 38px 1fr;
    border: solid 1.5px #eeeeee;
}

.valores__span {
    display: block;
    text-align: center;
    padding: .6em;
    color: #eeeeee;
}

.valores__text {
    display: block;
    width: 100%;
    padding: .6em;
}

.opciones {
    display: grid;
    margin: 2em auto 0;
    grid-template-columns: 90px 90px 90px;
    grid-gap: 1em;
    justify-content: center;
}

.opciones__button {
    cursor: pointer;
    display: block;
    text-align: center;
    border: none;
    border: solid 1.5px #eeeeee;
    background-color: transparent;
    font-size: 14px;
    color: #eeeeee;
    padding: .8em;
    border-radius: 3px;
}

.opciones__button:hover {
    background-color: #eeeeee;
    color: #18191a;
}

.opciones__button:active {
    transform: scale(.96);
}

.resultado {
    width: 100%;
    margin: 1.5em auto 0;
    display: grid;
    grid-gap: 2em;
    margin-bottom: 3em;
}

.resultado__pro,
.resultado__reg,
.resultado__cen {
    background-color: #eeeeee;
    width: 100%;
    display: block;
    text-align: center;
    border-radius: 3px;
    box-shadow: 0px 5px 2px -5px #eeeeee;
}

.resultado h4 {
    font-size: 15px;
    letter-spacing: .7px;
    padding: .5em;
    color: #18191a;
}

.resultado p {
    padding: .5em;
    color: #18191a;
}
</style>