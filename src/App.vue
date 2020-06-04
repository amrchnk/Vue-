<template>
  <div id="app">
    <Lab/>
  </div>
</template>

<script>

import Lab from '@/components/lab'
export default {
  name:'App',
  components:{
    Lab
  }
};
</script>

<style>
  body{
      font-size: 15px !important;
  }
  
  button{
      font-size: 15px !important;
  }
  
  .form {
      width: 400px;
      margin: auto auto;
      margin-top: 50px;
      border: 0.5px solid #E5E5E5;
      padding: 20px 25px;
      border-radius: 10px;
  
  }
  
  .note{
    display: flex;
      flex-direction: column;
      align-items: center;
  }
  
  .check{
      margin-top: 15px;
  }
  
  .note-in{
    margin-top: 30px;
      float: left;
  }
  
  .features{
      float: right;
      display: flex;
  }
  
  .field {
      margin-top: 5px;
      clear:both; 
      text-align:right;
  }
  
  label {
      float:left;
      padding-right:10px;
  }
  
   p input[type='checkbox'] {
   margin-right: 10px;
  }
  .best{
    margin-left: 15px;
  }
  
  input {
      margin-left: -15px;
  }
  
  span{
      color: yellow;
      margin-left: 10px;
  }
  
  
  
  li {
      list-style-type: none;
      display: flex;
  }
  
  .delete {
      cursor: pointer;
      text-decoration: none;
      display: block;
      width: 20px;
      height: 20px;
      margin-left: 10px;
  }
  
  .delete:hover {
      transition: all 0.5s;
  }
  
  .radio{
    margin-top: 15px;
  }
</style>
