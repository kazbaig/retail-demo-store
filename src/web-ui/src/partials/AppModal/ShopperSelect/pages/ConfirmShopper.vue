<template>
  <div :class="{ mobile: isMobile }">
    <h1 class="confirm-shopper mb-4 text-center">Confirm shopper</h1>

    <div class="flex-container mb-5 d-flex">
      <div class="your-selections px-4 py-3">
        <h2 class="your-selections-heading mb-4 text-center">
          Your selections
        </h2>
        <dl class="selections">
          <dt class="key">Age range:</dt>
          <dd>{{ selection.ageRange }}</dd>

          <dt class="key">Primary interest:</dt>
          <dd>{{ selection.primaryInterest }}</dd>
        </dl>
      </div>

      <div class="assigned-shopper px-4 py-3">
        <h2 class="assigned-shopper-heading mb-4 text-center">
          Assigned shopper
        </h2>

        <div class="mb-3">
          {{ assignedShopper.name }}. {{ assignedShopper.gender }}. {{ assignedShopper.age }} years
        </div>

        <dl>
          <div class="mb-2 d-flex flex-wrap">
            <dt class="mr-1">Primary interest:</dt>
            <dd class="mb-0">{{ assignedShopper.primaryInterest }}</dd>
          </div>

          <div>
            <div class="d-flex flex-wrap">
              <dt class="mr-1">Secondary interest{{ assignedShopper.secondaryInterests.length > 1 ? 's' : '' }}:</dt>
              <dd class="mb-0">
                {{
                  [
                    assignedShopper.secondaryInterests
                      .slice(0, assignedShopper.secondaryInterests.length - 1)
                      .join(', '),
                    assignedShopper.secondaryInterests[assignedShopper.secondaryInterests.length - 1],
                  ].join(' and ')
                }}
              </dd>
            </div>
            <div class="right">
              <a
                href="#"
                type="button"
                class="learn-more"
                data-toggle="tooltip"
                data-placement="bottom"
                title="Secondary interests are randomly selected for you and have a lower impact on the recommendations the system produces."
                ref="learnMore"
              >
                Learn more
              </a>
            </div>
          </div>
        </dl>
      </div>
    </div>

    <div class="button-container d-flex">
      <button class="try-again btn btn-outline-primary" @click="openGetStartedPage">Try again</button>
      <button class="confirm btn btn-primary" @click="confirmShopper">Confirm shopper</button>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

import { APP_MODAL_ID } from '../../config';

export default {
  name: 'ConfirmShopper',
  computed: {
    ...mapState({
      isMobile: (state) => state.modal.isMobile,
      selection: (state) => state.modal.openModal.selection,
      assignedShopper: (state) => state.modal.openModal.assignedShopper,
    }),
  },
  mounted() {
    // eslint-disable-next-line no-undef
    $(this.$refs.learnMore).tooltip();
  },
  beforeDestroy() {
    // eslint-disable-next-line no-undef
    $(this.$refs.learnMore).tooltip('dispose');
  },
  methods: {
    ...mapActions(['openGetStartedPage']),
    confirmShopper() {
      // eslint-disable-next-line no-undef
      $(`#${APP_MODAL_ID}`).modal('hide');
    },
  },
};
</script>

<style scoped>
.confirm-shopper {
  font-size: 1.75rem;
}

.mobile .flex-container {
  flex-direction: column;
}

.your-selections,
.assigned-shopper {
  flex: 1;
  border: 1px solid var(--grey-400);
  border-radius: 4px;
}

.your-selections {
  margin-right: 24px;
  font-size: 1.25rem;
}

.your-selections-heading {
  font-size: 1.75rem;
}

.mobile .your-selections {
  margin-right: 0;
  margin-bottom: 24px;
}

.selections {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-row-gap: 8px;
  grid-column-gap: 16px;
}

.key {
  justify-self: end;
  font-weight: normal;
  color: var(--grey-600);
}

.assigned-shopper {
  font-size: 1.5rem;
}

.assigned-shopper-heading {
  font-size: 1.75rem;
}

.learn-more {
  font-style: italic;
  font-size: 0.9rem;
  color: var(--blue-600);
}

.button-container {
  justify-content: flex-end;
}

.mobile .button-container {
  flex-direction: column;
  align-items: center;
}

.try-again,
.confirm {
  width: 200px;
  font-size: 1.25rem;
}

.try-again:hover,
.try-again:focus,
.confirm:hover,
.confirm:focus {
  border-color: var(--blue-600);
  background: var(--blue-600);
  color: var(--white);
}

.mobile .try-again, .mobile .confirm {
  width: 100%;
  max-width: 350px;
}

.try-again {
  margin-right: 8px;
  border-color: var(--blue-500);
  color: var(--blue-500);
}

.mobile .try-again {
  margin-right: 0;
  margin-bottom: 8px;
}

.confirm {
  border-color: var(--blue-500);
  background: var(--blue-500);
}
</style>
