<template>
  <Modal>
    <template #body="{bodyClass}">
      <component :is="currentPageComponent" :class="[bodyClass, 'shopper-select-page', isMobile ? 'shopper-select-page--mobile' : '']"></component>
    </template>
  </Modal>
</template>

<script>
import { mapState } from 'vuex';

import Modal from '../Modal/Modal';
import GetStarted from './pages/GetStarted';
import SelectShopper from './pages/SelectShopper';
import ConfirmShopper from './pages/ConfirmShopper';
import { ShopperSelectPages } from './config';

export default {
  name: 'DemoWalkthrough',
  components: {
    Modal,
  },
  computed: {
    ...mapState({ currentPage: (state) => state.modal.openModal.currentPage, isMobile: state => state.modal.isMobile }),
    currentPageComponent() {
      switch (this.currentPage) {
        case ShopperSelectPages.GetStarted:
          return GetStarted;
        case ShopperSelectPages.SelectShopper:
          return SelectShopper;
        case ShopperSelectPages.ConfirmShopper:
          return ConfirmShopper;
      }

      throw new Error('Invalid current page on shopper select modal');
    },
  },
};
</script>

<style scoped>
.shopper-select-page {
  overflow: auto;
  padding: 16px 48px;
}

.shopper-select-page--mobile {
  padding: 16px;
  padding-top: 0px;
}
</style>

<style>
.tooltip .tooltip-inner {
  background: var(--blue-600);
  padding: 16px 8px;
  min-width: 300px;
}

.tooltip.bs-tooltip-bottom .arrow::before {
  border-bottom-color: var(--blue-600);
}

.tooltip a {
  text-decoration: underline;
  color: var(--white);
}
</style>
