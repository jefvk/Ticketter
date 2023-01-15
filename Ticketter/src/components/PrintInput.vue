<template>
  <div>
    <h1>Titel</h1>
    <p>{{ name }}</p>
    <button @click="print()">print</button>
  </div>
</template>
<script>
// const ThermalPrinter = require("../node-thermal-printer").printer;
// const PrinterTypes = require("../node-thermal-printer").types;

import { ThermalPrinter, PrinterTypes } from "node-thermal-printer";
export default {
  name: "PrintInput",
  data() {
    return {
      name: "jefke",
    };
  },
  methods: {
    async print() {
      let printer = new ThermalPrinter({
        type: PrinterTypes.EPSON,
        interface: "tcp://xxx.xxx.xxx.xxx",
      });

      printer.alignCenter();
      printer.println("Hello world");
      printer.cut();
      try {
        printer.execute();
        console.error("Print done!");
      } catch (error) {
        console.log("Print failed:", error);
      }
    },
  },
};
</script>
<style lang="scss"></style>
