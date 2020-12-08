<template>
  <div :class="{ mobile: isMobile }">
    <h1 class="heading mb-5 text-center">Select A Shopper</h1>
    <div class="button-container d-flex justify-content-center">
      <button
        type="button"
        class="auto-select btn btn-lg btn-outline-primary"
        @click="autoSelectShopper"
        data-toggle="tooltip"
        data-placement="bottom"
        title="This option will allow you to select an existent shopper based on demographics and shopping preferences"
        ref="autoSelectShopper"
      >
        Auto select shopper
      </button>
      <button
        type="button"
        class="choose-shopper btn btn-lg btn-primary"
        @click="chooseAShopper"
        data-toggle="tooltip"
        data-placement="bottom"
        title="This option randomly selects a shopper from the available store users in the current Retail Demo Store users dataset"
        ref="chooseAShopper"
      >
        Choose a shopper
      </button>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';

import { RepositoryFactory } from '@/repositories/RepositoryFactory';

const UsersRepository = RepositoryFactory.get('users');

export default {
  name: 'GetStarted',
  computed: {
    ...mapState({ isMobile: (state) => state.modal.isMobile }),
  },
  mounted() {
    // eslint-disable-next-line no-undef
    $([this.$refs.autoSelectShopper, this.$refs.chooseAShopper]).tooltip();
  },
  beforeDestroy() {
    // eslint-disable-next-line no-undef
    $([this.$refs.autoSelectShopper, this.$refs.chooseAShopper]).tooltip('dispose');
  },
  methods: {
    chooseAShopper() {
      this.$emit('chooseAShopper');
    },
    async autoSelectShopper() {
      const { data } = await UsersRepository.getRandomUser();

      this.$emit('autoSelectShopper', {
        assignedShopper: data,
      });
    },
  },
};
</script>

<style scoped>
.heading {
  margin-top: 20%;
  font-size: 1.75rem;
}

.mobile .button-container {
  flex-direction: column;
  align-items: center;
}

.auto-select,
.choose-shopper {
  width: 300px;
}

.mobile .auto-select,
.mobile .choose-shopper {
  width: 100%;
  max-width: 350px;
}

.auto-select {
  margin-right: 16px;
  border-color: var(--blue-500);
  color: var(--blue-500);
}

.mobile .auto-select {
  margin-right: 0px;
  margin-bottom: 16px;
}

.choose-shopper {
  background-color: var(--blue-500);
  border-color: var(--blue-500);
}

.auto-select:hover,
.auto-select:focus,
.choose-shopper:hover,
.choose-shopper:focus {
  background-color: var(--blue-600);
  border-color: var(--blue-600);
  color: var(--white);
}
</style>
