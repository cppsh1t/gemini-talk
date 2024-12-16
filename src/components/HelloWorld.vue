<template>
  <div style="display: flex; gap: 20px">
    Your Token <el-input v-model="token"></el-input>
    <el-button @click="initAI">确定</el-button>
  </div>
  <p>{{ msg }}</p>
  <div class="container">
    <el-input v-model="prompt"></el-input>
    <el-button @click="send">发送</el-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const msg = ref("");
import { GoogleGenerativeAI } from "@google/generative-ai";

const token = ref("");
let genAI = new GoogleGenerativeAI(token.value);
let model = genAI.getGenerativeModel({ model: "gemini-1.5-flash" });
const prompt = ref("");

async function initAI() {
  genAI = new GoogleGenerativeAI(token.value);
  model = genAI.getGenerativeModel({ model: "gemini-1.5-flash" });
  console.log("init finish");
}

async function send() {
  console.log(
    token.value === "AIzaSyAR9CqlpuGuQyCJ2ySKFZnULY-rhPa1y2g",
    token.value
  );
  const result = await model.generateContent(prompt.value);
  msg.value = result.response.text();
  prompt.value = "";
}
</script>

<style scoped>
.container {
  display: flex;
  gap: 20px;
}
</style>
