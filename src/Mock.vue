<template></template>
<style></style>
<script>
import Mock from "mockjs";
export default {
  created() {
    Mock.mock('/hello.json', {
      "list|1-10": [
        {
          "id|+1": 1,
          email: "@EMAIL"
        }
      ]
    });
  }
};
</script>