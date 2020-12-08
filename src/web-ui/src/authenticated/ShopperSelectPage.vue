<template>
  <SecondaryLayout>
    <div class="container">
      <ShopperSelect @confirm="onConfirm"></ShopperSelect>
    </div>
  </SecondaryLayout>
</template>

<script>
import SecondaryLayout from '@/components/SecondaryLayout/SecondaryLayout';
import ShopperSelect from '@/partials/ShopperSelect/ShopperSelect';

export default {
  name: 'ShopperSelectPage',
  components: { SecondaryLayout, ShopperSelect },
  methods: {
    onConfirm() {
      this.$router.push('/');
    },
  },
};
</script>

<style></style>
