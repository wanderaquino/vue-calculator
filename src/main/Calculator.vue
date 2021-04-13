<template>
    <div class="calculator">
        <Display value="10000"/>
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
        <Button @onButtonClick="addDigit" label="3"/>
        <Button @onButtonClick="addDigit" label="3"/>
        <Button @onButtonClick="setOperation" label="+" operation/>
        <Button @onButtonClick="addDigit" label="0" double/>
        <Button @onButtonClick="addDigit" label=","/>
        <Button @onButtonClick="setOperation" label="=" operation/>
    </div>

</template>

<script>
import Display from "../components/Display";
import Button from "../components/Button";

export default {
    components: {Button, Display},
    methods: {
        clearMemory() {
            console.log("Limpar Memória");
        },

        setOperation (operation) {
            console.log(`Operation  ${operation}`);
        },
        addDigit(n) {
            console.log("Add Digit "+ n);
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