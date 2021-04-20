<template>
  <div class="progress">
    <h4>{{ progress }}</h4>
    <h4>{{ percent }} %</h4>
  </div>
</template>
<script>
const thisYear = new Date().getFullYear();
const startTimeOfThisYear = new Date(
  `${thisYear}-01-01T00:00:00+00:00`
).getTime();
const endTimeOfThisYear = new Date(
  `${thisYear}-12-31T23:59:59+00:00`
).getTime();
const progressOfThisYear =
  (Date.now() - startTimeOfThisYear) /
  (endTimeOfThisYear - startTimeOfThisYear);

export default {
  data() {
    return {
      percent: null,
      progress: null
    };
  },
  methods: {
    generateProgressBar() {
      const progressBarCapacity = 30;
      const passedProgressBarIndex = parseInt(
        progressOfThisYear * progressBarCapacity
      );
      const progressBar = Array(progressBarCapacity)
        .fill("▁")
        .map((value, index) => (index < passedProgressBarIndex ? "█" : value))
        .join("");
      return `⏳ ${progressBar}`;
    }
  },
  mounted() {
    this.progress = this.generateProgressBar();
    this.percent = (progressOfThisYear * 100).toFixed(2);
  }
};
</script>
<style scoped>
.progress {
  width: 100%;
  max-width: 100%;
  margin: auto;
  align-items: center;
  height: 100vh;
  display: flex;
  justify-content: center;
}
</style>
