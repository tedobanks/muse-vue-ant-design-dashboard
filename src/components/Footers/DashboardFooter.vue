<template>
  <a-layout-footer>
    <a-row type="flex">
      <a-col :span="24" :md="12">
        <p class="copyright">
          &copy; {{ currentYear }} Tabula Rasa Stays. All rights reserved.
        </p>
        </a-col>
      </a-row>
  </a-layout-footer>
  </template>

<script>
export default {
  data() {
    return {
      // Get the current year dynamically
      currentYear: new Date().getFullYear(),
    };
  },
};
</script>