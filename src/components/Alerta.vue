<script lang="ts" setup></script>

<template>
  <div class="alerta">
    <slot> </slot>
  </div>
</template>

<style lang="css" scoped>
.alerta {
  padding: 1rem;
  font-weight: 900;
  text-transform: uppercase;
  font-size: 1.7rem;
  text-align: center;
  background: #d3cce3; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #e9e4f0,
    #d3cce3
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #e9e4f0,
    #d3cce3
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  color: #ec0d0d;
  border-left: 0.5rem solid #ec0d0d;
  -webkit-box-shadow: 6px 13px 5px 0px rgba(0, 0, 0, 0.29);
  -moz-box-shadow: 6px 13px 5px 0px rgba(0, 0, 0, 0.29);
  box-shadow: 6px 13px 5px 0px rgba(0, 0, 0, 0.29);
  border-radius: 2rem;
  margin-bottom: 2.5rem;
}
</style>
