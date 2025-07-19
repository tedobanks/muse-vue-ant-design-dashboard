<template>
    <a-card :bordered="false" class="header-solid h-full" :bodyStyle="{padding: 0,}">
        <template #title>
            <a-row type="flex" align="middle">
                <a-col :span="24" :md="12">
                    <h5 class="font-semibold m-0">Manage Admins</h5>
                </a-col>
                <a-col :span="24" :md="12" style="display: flex; align-items: center; justify-content: flex-end">
                    <a-radio-group v-model="authorsHeaderBtns" size="small">
                        <a-radio-button value="all">ALL</a-radio-button>
                        <a-radio-button value="online">ONLINE</a-radio-button>
                    </a-radio-group>
                </a-col>
            </a-row>
        </template>
        <a-table :columns="columns" :data-source="data" :pagination="false">

            <template slot="author" slot-scope="author">
                <div class="table-avatar-info">
                    <a-avatar shape="square" :src="author.avatar" />
                    <div class="avatar-info">
                        <h6>{{ author.name }}</h6>
                        <p>{{ author.email }}</p>
                    </div>
                </div>
            </template>

            <template slot="func" slot-scope="func">
                <div class="author-info">
                    <h6 class="m-0">{{ func.job }}</h6>
                    <p class="m-0 font-regular text-muted">{{ func.department }}</p>
                </div>
            </template>

            <template slot="editBtn" slot-scope="row">
                <a-button type="link" :data-id="row.key" class="btn-edit">
                    Edit
                </a-button>
            </template>

        </a-table>
    </a-card>
    </template>

<script>

    export default ({
        props: {
            data: {
                type: Array,
                default: () => [],
            },
            columns: {
                type: Array,
                default: () => [],
            },
        },
        data() {
            return {
                // Active button for the "Authors" (now "Manage Admins") table's card header radio button group.
                authorsHeaderBtns: 'all',
            }
        },
    })

</script>

<style lang="scss">
/* Any component-specific styles would go here */
.tag-status {
    /* If you still use ant-tag-primary or ant-tag-muted elsewhere, keep their definitions.
       Otherwise, this specific styling for 'tag-status' related to the removed 'status' column
       might become redundant if not used for other purposes. */
}
</style>