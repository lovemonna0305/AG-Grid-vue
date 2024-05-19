<template>
  <div class="custom-header">
    <span>{{ params.displayName }}</span>
  </div>
</template>

<script>
export default {
  props: {
    params: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      inputValue: "120",
    };
  },
  methods: {
    handleButtonClick() {
      console.log("Button clicked");
    },
  },
};
</script>

<style scoped>
.custom-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 12px;
  background-color: #f1f1f1;
  border-bottom: 1px solid #ddd;
}

.custom-header span {
  font-weight: bold;
}

.custom-header button {
  padding: 6px 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.custom-header input {
  padding: 6px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.custom-header a {
  color: #007bff;
  text-decoration: none;
}
</style>