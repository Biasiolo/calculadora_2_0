<template>
    <div class="container mt-2">
        <div class="card mx-auto" style="max-width: 400px;">
            <div class="card-body text-white fw-4">
                <h1 class="card-title text-center text-success">RB-420C</h1>
                <div class="mb-3 text-center">
                    <div class="display p-2 rounded">
                        <h3 class="text-monospace">{{ equation || '0' }}</h3>
                        <h2 class="text-monospace">{{ result }}</h2>
                    </div>
                </div>
                <div class="calculator-buttons">
                    <button class="btn btn-danger" @click="clear">C</button>
                    <button class="btn btn-light" @click="deleteLast">DEL</button>
                    <button class="btn btn-light" @click="addToEquation('/')">÷</button>
                    <button class="btn btn-light" @click="addToEquation('*')">×</button>

                    <button class="btn btn-light" @click="addToEquation('7')">7</button>
                    <button class="btn btn-light" @click="addToEquation('8')">8</button>
                    <button class="btn btn-light" @click="addToEquation('9')">9</button>
                    <button class="btn btn-light" @click="addToEquation('-')">-</button>

                    <button class="btn btn-light" @click="addToEquation('4')">4</button>
                    <button class="btn btn-light" @click="addToEquation('5')">5</button>
                    <button class="btn btn-light" @click="addToEquation('6')">6</button>
                    <button class="btn btn-light" @click="addToEquation('+')">+</button>

                    <button class="btn btn-light" @click="addToEquation('1')">1</button>
                    <button class="btn btn-light" @click="addToEquation('2')">2</button>
                    <button class="btn btn-light" @click="addToEquation('3')">3</button>
                    <button class="btn btn-primary" @click="calculate">=</button>

                    <button class="btn btn-light"  @click="addToEquation('0')">0</button>
                    <button class="btn btn-light" @click="addToEquation('.')">.</button>
                    <button class="btn btn-success" style="grid-column: span 2;" @click="storeResult">Enter</button>
                    <a href="https://github.com/Biasiolo/calculadora_2_0" class="btn btn-dark" target="_blank" style="grid-column: span 4;">Sobre</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            equation: '',
            result: '',
        };
    },
    methods: {
        addToEquation(input) {
            if (this.equation.length < 16) {
                this.equation += input;
            }
        },
        clear() {
            this.equation = '';
            this.result = '';
        },
        deleteLast() {
            this.equation = this.equation.slice(0, -1);
        },
        calculate() {
            try {
                const evaluation = eval(this.equation.replace(/×/g, '*').replace(/÷/g, '/'));
                this.result = parseFloat(evaluation.toFixed(4));
            } catch (error) {
                this.result = 'Erro';
            }
        },
        storeResult() {
            if (this.result !== '') {
                this.equation = this.result.toString();
                this.result = '';
            }
        },
    },
};
</script>
<style scoped>


.container {
    background-image: url(../assets/images/mesa.png);

    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 98vh;
}

.card {
    width: 100%;
    height: auto;
    background-color: #2d2d2d;
    border: 3px solid #222222;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.display {
    font-family: 'Courier New', Courier, monospace;
    font-size: 1.6em;
    background-color: rgba(139, 175, 192, 0.7); 
    backdrop-filter: blur(10px); 
    color: #0f0;
    padding: 8px;
    border-radius: 5px;
    text-align: right;
    height: 6.3rem;
    text-shadow: 0 0 10px rgba(0, 255, 0, 0.5); 
    border: 3px solid #222222;
    border-bottom: 2px solid rgb(73, 73, 73);
    white-space: nowrap; 
    overflow: hidden; 
    text-overflow: ellipsis; 
    align-items: center;
}

h1 {
    text-shadow: 0 0 6px #222222;; 
    font-family: 'Courier New', Courier, monospace;
    font-size: 2rem;
    font-weight: 500;
}

h3 {
    font-size: 2rem;
}
h2 {
    font-size: 2.3rem;
}

.calculator-buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    font-weight: 600;
    
}

button {
    padding: 16px;
    font-size: 1.2em;
    width:100%;
    border: 2px solid #222222;
    border-bottom: 1px solid #222222;
    border-left: 1px solid #222222;
}
</style>
