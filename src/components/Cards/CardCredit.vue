<template>
    <a-card class="card-balance header-solid h-full">
        <template #title>
            <div class="card-balance-header">
                <span class="text-white">Available balance</span>
                <a-tooltip title="This balance reflects transactions within the selected timespan.">
                    <a-icon type="info-circle" style="color: rgba(255, 255, 255, 0.7); margin-left: 8px;" />
                </a-tooltip>
            </div>
        </template>

        <h1 class="balance-amount">{{ formattedBalance }}</h1>

        <a-row type="flex" :gutter="[16, 16]" class="balance-filters">
            <a-col :span="24">
                <p class="filter-label">Quick Timespan:</p>
                <a-select default-value="all" style="width: 100%" @change="onTimespanChange" :value="selectedTimespan">
                    <a-select-option value="today">Today</a-select-option>
                    <a-select-option value="last7days">Last 7 Days</a-select-option>
                    <a-select-option value="last30days">Last 30 Days</a-select-option>
                    <a-select-option value="all">All Time</a-select-option>
                </a-select>
            </a-col>
        </a-row>
    </a-card>
    </template>

<script>
import moment from 'moment';

// Mock transaction data to simulate dynamic balance changes
const mockTransactions = [
    // Ensure the sum of 'all' transactions equals 435400.54 for initial display
    { date: '2025-07-18', amount: 1500.25 },
    { date: '2025-07-18', amount: -50.75 },
    { date: '2025-07-18', amount: -120.00 },
    { date: '2025-07-17', amount: 750.50 },
    { date: '2025-07-16', amount: -200.00 },
    { date: '2025-07-15', amount: 300.00 },
    { date: '2025-07-14', amount: -80.00 },
    { date: '2025-07-13', amount: 1000.00 },
    { date: '2025-07-12', amount: -30.00 },
    { date: '2025-07-10', amount: 2000.00 },
    { date: '2025-07-05', amount: -150.00 },
    { date: '2025-06-25', amount: 5000.00 },
    { date: '2025-06-20', amount: -300.00 },
    { date: '2025-05-10', amount: 10000.00 },
    { date: '2025-04-01', amount: -500.00 },
    { date: '2024-12-01', amount: 416071.54 }, // Adjusted to make total sum match 435400.54
    { date: '2024-11-15', amount: -100.00 },
];

export default {
    data() {
        return {
            totalAvailableBalance: 0, // This will be dynamically updated
            selectedTimespan: 'all',
            mockTransactions: mockTransactions, // Make mockTransactions available in data
        };
    },
    computed: {
        formattedBalance() {
            // Ensure the number is formatted correctly
            return `$ ${this.totalAvailableBalance.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 })}`;
        }
    },
    methods: {
        calculateBalanceForTimespan(value) {
            let startDate = null;
            let endDate = moment().endOf('day'); // End of today

            switch (value) {
                case 'today':
                    startDate = moment().startOf('day');
                    break;
                case 'last7days':
                    startDate = moment().subtract(6, 'days').startOf('day'); // Includes today
                    break;
                case 'last30days':
                    startDate = moment().subtract(29, 'days').startOf('day'); // Includes today
                    break;
                case 'all':
                default:
                    startDate = null; // No specific start date for 'all'
                    endDate = null; // No specific end date for 'all'
                    break;
            }

            let filteredTransactions = [];
            if (value === 'all') {
                filteredTransactions = this.mockTransactions;
            } else {
                filteredTransactions = this.mockTransactions.filter(transaction => {
                    const transactionDate = moment(transaction.date);
                    return transactionDate.isSameOrAfter(startDate, 'day') && transactionDate.isSameOrBefore(endDate, 'day');
                });
            }

            // Sum the amounts of the filtered transactions
            const sum = filteredTransactions.reduce((acc, transaction) => acc + transaction.amount, 0);
            this.totalAvailableBalance = sum;
        },
        onTimespanChange(value) {
            this.selectedTimespan = value;
            this.calculateBalanceForTimespan(value); // Recalculate balance when filter changes
            console.log('Selected Timespan:', value, 'New Balance:', this.totalAvailableBalance);
        },
    },
    created() {
        // Initialize the balance on component load to "All Time"
        this.calculateBalanceForTimespan('all');
    }
};
</script>

<style lang="scss">
.card-balance {
    background: linear-gradient(to right, #B1D5AC, #464A32) !important;
    color: #fff; // Ensure text is visible on the dark background
    border-radius: 8px; // Maintain rounded corners

    .ant-card-head {
        border-bottom: none; // Remove default border
        padding-bottom: 0;
        .ant-card-head-wrapper {
            .ant-card-extra {
                padding: 0;
            }
        }
    }

    .ant-card-body {
        padding: 24px; // Increased padding for more general space
        padding-top: 0; // Keep header content close to top
    }

    .card-balance-header {
        display: flex;
        align-items: center;
        font-size: 1rem;
        font-weight: 500;
        margin-bottom: 8px;
    }

    .balance-amount {
        font-size: 2.8rem;
        font-weight: bold;
        line-height: 1.2;
        margin-bottom: 24px;
        color: #fff; /* Explicitly set the color to white for the amount */
    }

    .balance-filters {
        .filter-label {
            color: rgba(255, 255, 255, 0.8);
            font-size: 0.85rem;
            margin-bottom: 4px;
        }
        .ant-select {
            width: 100%;

            .ant-select-selection {
                background-color: rgba(255, 255, 255, 0.1);
                border: 1px solid rgba(255, 255, 255, 0.2);
                color: #fff; // Text inside the select box
                .ant-select-selection__rendered {
                    color: #fff; // For selected value text
                }
            }
            .ant-select-arrow,
            .ant-select-selection__clear {
                color: rgba(255, 255, 255, 0.7);
            }
        }
        // Darker dropdown background for Ant Design Select
        .ant-select-dropdown {
            background-color: #363a2a !important; /* Slightly darker than gradient start */
            .ant-select-dropdown-menu-item {
                color: rgba(255, 255, 255, 0.8);
                &:hover:not(.ant-select-dropdown-menu-item-disabled) {
                    background-color: rgba(255, 255, 255, 0.1);
                }
                &.ant-select-dropdown-menu-item-selected {
                    background-color: rgba(255, 255, 255, 0.2);
                    color: #fff;
                }
            }
        }
    }
}
</style>