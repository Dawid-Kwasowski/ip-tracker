<template>
  <div class="location-card">
    <div class="location-card__info row">
      <div class="col">
        <h5>Adres IP</h5>
        <span>{{ ipAddress }}</span>
      </div>
      <div class="col">
        <h5>Region</h5>
        <span>{{ city }} | {{ country }}</span>
      </div>
      <div class="col">
        <h5>ISP</h5>
        <span>{{ isp }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["ipAddress", "city", "country", "isp"],
};
</script>

<style lang="scss">
.location-card {
  background: white;
  padding: 30px;
}
</style>
