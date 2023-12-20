<template>
  <div>
    <h1>Welcome</h1>
    <div>
      <input type="radio" name="options">
      <label>Answer</label><br>
      <input type="radio" name="options">
      <label>Answer</label><br>
    </div>
    <button type="submit">Send</button>
  </div>
  
</template>

<script>

export default {
  name: 'App',

  components: {

  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: black;
  margin: 60px auto;
  max-width: 600px;
}

input {
    margin: 10px;
}

 button {
    margin-top: 10px;
    background-color: white; 
    color: black; 
    border: 2px solid #008CBA;
    border-radius: 4px;
    padding: 5px 24px;
}

button:hover {
    background-color: #008CBA;
    color: white;
    cursor: pointer;
}



</style>
