<template>
    <div>

        <div class="profile-nav-bg" style="background-color: #464A32"></div>
        <a-card :bordered="false" class="card-profile-head" :bodyStyle="{padding: 0,}">
            <template #title>
                <a-row type="flex" align="middle">
                    <a-col :span="24" :md="12" class="col-info">
                        <a-avatar :size="74" shape="square" src="images/face-1.jpg" />
                        <div class="avatar-info">
                            <h4 class="font-semibold m-0">Sarah Jacob</h4>
                            <p>CEO / Co-Founder</p>
                        </div>
                    </a-col>
                    <a-col :span="24" :md="12" style="display: flex; align-items: center; justify-content: flex-end">
                        <a-radio-group v-model="profileHeaderBtns" size="small">
                            <a-radio-button value="overview">OVERVIEW</a-radio-button>
                            <a-radio-button value="teams">TEAMS</a-radio-button>
                            <a-radio-button value="projects">PROJECTS</a-radio-button>
                        </a-radio-group>
                    </a-col>
                </a-row>
            </template>
        </a-card>
        <a-row :gutter="24" type="flex">
            <a-col :span="24" class="mb-24">
                <CardAuthorTable
                    :data="table1Data"
                    :columns="table1Columns"
                ></CardAuthorTable>
            </a-col>
        </a-row>
    </div>
</template>

<script>
    import CardAuthorTable from "../components/Cards/CardAuthorTable"; // Import the CardAuthorTable component

    // Updated "Authors" table list of columns and their properties - removed STATUS and EMPLOYED columns
    const table1Columns = [
        {
            title: 'AUTHOR',
            dataIndex: 'author',
            scopedSlots: { customRender: 'author' },
        },
        {
            title: 'FUNCTION',
            dataIndex: 'func',
            scopedSlots: { customRender: 'func' },
        },
        {
            title: '',
            scopedSlots: { customRender: 'editBtn' },
            width: 50,
        },
    ];

    // Updated "Authors" table list of rows and their properties - removed status and employed fields
    const table1Data = [
        {
            key: '1',
            author: {
                avatar: 'images/face-2.jpg',
                name: 'Michael John',
                email: 'michael@mail.com',
            },
            func: {
                job: 'Manager',
                department: 'Organization',
            },
        },
        {
            key: '2',
            author: {
                avatar: 'images/face-3.jpg',
                name: 'Alexa Liras',
                email: 'alexa@mail.com',
            },
            func: {
                job: 'Programator',
                department: 'Developer',
            },
        },
        {
            key: '3',
            author: {
                avatar: 'images/face-1.jpg',
                name: 'Laure Perrier',
                email: 'laure@mail.com',
            },
            func: {
                job: 'Executive',
                department: 'Projects',
            },
        },
        {
            key: '4',
            author: {
                avatar: 'images/face-4.jpg',
                name: 'Miriam Eric',
                email: 'miriam@mail.com',
            },
            func: {
                job: 'Marketing',
                department: 'Organization',
            },
        },
        {
            key: '5',
            author: {
                avatar: 'images/face-5.jpeg',
                name: 'Richard Gran',
                email: 'richard@mail.com',
            },
            func: {
                job: 'Manager',
                department: 'Organization',
            },
        },
        {
            key: '6',
            author: {
                avatar: 'images/face-6.jpeg',
                name: 'John Levi',
                email: 'john@mail.com',
            },
            func: {
                job: 'Tester',
                department: 'Developer',
            },
        },
    ];

    export default ({
        components: {
            CardAuthorTable, // Register the imported component
        },
        data() {
            return {
                // Active button for the "User Profile" card's radio button group.
                profileHeaderBtns: 'overview',

                // Data for the Authors Table, now using the simplified structure
                table1Data,
                table1Columns,
            }
        },
    })

</script>

<style lang="scss">
/* You can add specific styles for the Authors Table here if needed */
</style>