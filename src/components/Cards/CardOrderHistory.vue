<template>
  <a-card
    :bordered="false"
    class="header-solid h-full"
    :bodyStyle="{ paddingTop: '12px' }"
  >
    <template #title>
      <h6>Orders History</h6>
      <p>this month <span class="text-success">+20%</span></p>
    </template>
    <a-timeline pending="Recording..." :reverse="timelineReverse">
      <a-timeline-item color="green">
        $2,400 - Redesign store
        <p>09 JUN 7:20 PM</p>
      </a-timeline-item>
      <a-timeline-item color="green">
        New order #3654323
        <p>08 JUN 12:20 PM</p>
      </a-timeline-item>
      <a-timeline-item color="blue">
        Company server payments
        <p>04 JUN 3:10 PM</p>
      </a-timeline-item>
      <a-timeline-item color="blue">
        New card added for order #4826321
        <p>02 JUN 2:45 PM</p>
      </a-timeline-item>
      <a-timeline-item color="blue">
        Unlock folders for development
        <p>18 MAY 1:30 PM</p>
      </a-timeline-item>
      <a-timeline-item color="gray">
        New order #46282344
        <p>14 MAY 3:30 PM</p>
      </a-timeline-item>
      <template #pendingDot> </template>
    </a-timeline>
    <a-button
      type="primary"
      block
      size="small"
      @click="toggleTimelineAndNavigate"
    >
      <svg
        v-show="!timelineReverse"
        width="16"
        height="16"
        viewBox="0 0 20 20"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M3 3C2.44772 3 2 3.44772 2 4C2 4.55228 2.44772 5 3 5H14C14.5523 5 15 4.55228 15 4C15 3.44772 14.5523 3 14 3H3Z"
          fill="#111827"
        />
        <path
          d="M3 7C2.44772 7 2 7.44772 2 8C2 8.55228 2.44772 9 3 9H8C8.55228 9 9 8.55228 9 8C9 7.44772 8.55228 7 8 7H3Z"
          fill="#111827"
        />
        <path
          d="M3 11C2.44772 11 2 11.4477 2 12C2 12.5523 2.44772 13 3 13H7C7.55228 13 8 12.5523 8 12C8 11.4477 7.55228 11 7 11H3Z"
          fill="#111827"
        />
        <path
          d="M13 3C13 2.44772 13.4477 2 14 2C14.5523 2 15 2.44771 15 3L15 8.58579L16.2929 7.29289C16.6834 6.90237 17.3166 6.90237 17.7071 7.29289C18.0976 7.68342 18.0976 8.31658 17.7071 8.70711L14.7071 11.7071C14.5196 11.8946 14.2652 12 14 12C13.7348 12 13.4804 11.8946 13.2929 11.7071L10.2929 8.70711C9.90237 8.31658 9.90237 7.68342 10.2929 7.29289C10.6834 6.90237 11.3166 6.90237 11.7071 7.29289L13 8.58579L13 3Z"
          fill="#111827"
        />
      </svg>
      <svg
        v-show="timelineReverse"
        width="16"
        height="16"
        viewBox="0 0 20 20"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M3 3C2.44772 3 2 3.44772 2 4C2 4.55228 2.44772 5 3 5H14C14.5523 5 15 4.55228 15 4C15 3.44772 14.5523 3 14 3H3Z"
          fill="#111827"
        />
        <path
          d="M3 7C2.44772 7 2 7.44772 2 8C2 8.55228 2.44772 9 3 9H10C10.5523 9 11 8.55228 11 8C11 7.44772 10.5523 7 10 7H3Z"
          fill="#111827"
        />
        <path
          d="M3 11C2.44772 11 2 11.4477 2 12C2 12.5523 2.44772 13 3 13H7C7.55228 13 8 12.5523 8 12C8 11.4477 7.55228 11 7 11H3Z"
          fill="#111827"
        />
        <path
          d="M15 12C15 12.5523 14.5523 13 14 13C13.4477 13 13 12.5523 13 12L13 6.41421L11.7071 7.70711C11.3166 8.09763 10.6834 8.09763 10.2929 7.70711C9.90237 7.31658 9.90237 6.68342 10.2929 6.29289L13.2929 3.29289C13.4804 3.10536 13.7348 3 14 3C14.2652 3 14.5196 3.10536 14.7071 3.29289L17.7071 6.29289C18.0976 6.68342 18.0976 7.31658 17.7071 7.70711C17.3166 8.09763 16.6834 8.09763 16.2929 7.70711L15 6.41421L15 12Z"
          fill="#111827"
        />
      </svg>
      See all
    </a-button>
  </a-card>
  </template>

<script>
export default {
  data() {
    return {
      // Whether or not the timeline in "Orders History" card is reversed.
      timelineReverse: false,
    };
  },
  methods: {
    toggleTimelineAndNavigate() {
      // Toggle the timeline reverse state
      this.timelineReverse = !this.timelineReverse;

      // Navigate to the /payments route
      this.$router.push('/payments');
    }
  }
};
</script>