<template>
    <div>
        <a-row type="flex" :gutter="24">
            <a-col :span="24" :md="24">
                <a-row type="flex" :gutter="24">
                    <a-col :span="24" :xl="24" class="mb-24">
                        <CardCredit class="taller-credit-card"></CardCredit>
                    </a-col>
                </a-row>
            </a-col>
            </a-row>

        <a-row type="flex" :gutter="24">
            <a-col :span="24" :md="24" class="mb-24">
                <CardTransactions
                    :data="transactionsData"
                ></CardTransactions>
                </a-col>
            </a-row>
    </div>
</template>

<script>
    import CardCredit from "../components/Cards/CardCredit";
    import CardTransactions from "../components/Cards/CardTransactions";

    // "Your Transactions" list data.
    const transactionsData = [
        {
            period: "NEWEST",
        },
        {
            title: "Netflix",
            datetime: "27 March 2021, at 12:30 PM",
            amount: "2,500",
            type: -1, // 0 is for pending, 1 is for deposit, -1 is for withdrawal.
            status: 'danger',
        },
        {
            title: "Apple",
            datetime: "27 March 2021, at 04:30 AM",
            amount: "2,000",
            type: 1,
            status: 'success',
        },
        {
            period: "YESTERDAY",
        },
        {
            title: "Stripe",
            datetime: "26 March 2021, at 12:30 AM",
            amount: "750",
            type: 1,
            status: 'success',
        },
        {
            title: "HubSpot",
            datetime: "26 March 2021, at 11:30 AM",
            amount: "1,050",
            type: 1,
            status: 'success',
        },
        {
            title: "Creative Tim",
            datetime: "26 March 2021, at 07:30 AM",
            amount: "2,400",
            type: 1,
            status: 'success',
        },
        {
            title: "Webflow",
            datetime: "26 March 2021, at 04:00 AM",
            amount: "Pending",
            type: 0,
            status: 'warning',
        },
    ];

    export default {
        components: {
            CardCredit,
            CardTransactions,
        },
        data() {
            return {
                // Associating "Your Transactions" list data with its corresponding property.
                transactionsData,
            };
        },
    };
</script>

<style lang="scss">
// Styles to make the CardCredit component taller
.taller-credit-card {
    .ant-card-body {
        // You can adjust this min-height value as needed
        // For example, if the original height was ~150px, 225px would be 50% taller.
        min-height: 225px; /* Example: adjust this value to achieve desired height */
        display: flex;
        flex-direction: column;
        justify-content: center; /* Center content vertically if space allows */
    }
}
</style>