<template>
    <div class="calculator">
        <Display :value="displayValue" />
        <Button @onButtonClick="clearMemory" label="AC" triple/>
        <Button @onButtonClick="setOperation" label="/" operation/>
        <Button @onButtonClick="addDigit" label="7"/>
        <Button @onButtonClick="addDigit" label="8"/>
        <Button @onButtonClick="addDigit" label="9"/>
        <Button @onButtonClick="setOperation" label="*" operation/>
        <Button @onButtonClick="addDigit" label="4"/>
        <Button @onButtonClick="addDigit" label="5"/>
        <Button @onButtonClick="addDigit" label="6"/>
        <Button @onButtonClick="setOperation" label="-" operation/>
        <Button @onButtonClick="addDigit" label="1"/>
        <Button @onButtonClick="addDigit" label="2"/>
        <Button @onButtonClick="addDigit" label="3"/>
        <Button @onButtonClick="setOperation" label="+" operation/>
        <Button @onButtonClick="addDigit" label="0" double/>
        <Button @onButtonClick="addDigit" label="."/>
        <Button @onButtonClick="setOperation" label="=" operation/>
    </div>

</template>

<script>
import Display from "../components/Display";
import Button from "../components/Button";

export default {
    data: function () {
        return {
            displayValue: "0",
            clearedDisplay: false,
            operation: null,
            values: [0,0],
            currentValue: "0"
        }
    },
    components: {Button, Display},
    methods: {
        clearMemory() {
            //Fazer o objeto retornar ao estado originao: target <- source
            Object.assign(this.$data, this.$options.data());
        },

        setOperation (operation) {
            if (this.currentValue === 0) {
                this.operation = operation;
                this.currentValue = 1;
                this.clearedDisplay = true;
            } else {
                const equals = operation === "=";
                const currentOperation = this.operation;

                try {
                    this.values[0] = eval(`${this.values[0]} ${currentOperation} ${this.values[1]}`);
                }
                catch (e) {
                    this.$emit("onError", e);
                }

                this.values[1] = 0;
                this.displayValue = this.values[0];
                this.operation = equals ? null : operation;
                this.currentValue = equals ? 0 : 1;
                this.clearedDisplay = !equals;
            }
            console.log(`Operation  ${operation}`);
        },
        addDigit(n) {
            if (n === "." && this.displayValue.includes(".")){return}

            const clearedDisplay = this.displayValue === "0" || this.clearedDisplay;
            const currentValue = clearedDisplay ? "" : this.displayValue;
            const displayValue = currentValue + n;

            this.displayValue = displayValue;
            this.clearedDisplay = false;

            if (n !== ".") {
                const i = this.currentValue;
                const newValue = parseFloat(displayValue);
                this.values[i] = newValue;
            }
        }
    }
};

</script>

<style>

.calculator {
    width: 235px;
    height: 320px;
    border-radius: 5px;
    overflow:hidden;

    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}

</style>