<template>
    <v-layout row>
        <v-flex md3>
            <v-app style="background-color: grey lighten-1;" class="ma-n4">
                <v-container ml-5 mt-5>
                    <h4 class="mb-5">FILTERS</h4>
                    <v-list-item>
                        <v-list-item-action>
                            <v-icon small>fas fa-user-plus</v-icon>
                        </v-list-item-action>
                        <v-list-item-content>
                            <v-list-item-title>New Candidates</v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                    <v-list-item>
                        <v-list-item-action>
                            <v-icon small="">fas fa-user-tag</v-icon>
                        </v-list-item-action>
                        <v-list-item-content>
                            <v-list-item-title>Follower Candidate</v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                    <v-list-item>
                        <v-list-item-action>
                            <v-icon small>fas fa-user-cog</v-icon>
                        </v-list-item-action>
                        <v-list-item-content>
                            <v-list-item-title>Still in the running</v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                    <v-text-field label="Custom Search" prepend-icon="search" class="ml-3 mr-12"></v-text-field>
                    <v-select v-model="value" :items="items" chips attach clearable label="Keyword" multiple class="ml-3 mr-12"></v-select>
                    <v-select v-model="job" :items="jobs" chips attach clearable label="Jobs" multiple class="ml-3 mr-12"></v-select>

                </v-container>
            </v-app>
        </v-flex>
        <v-flex md9>
            <v-app style="background-color: white;" class="ma-n4">
                <v-container>
                    <template>
                        <v-data-table
                            v-model="selected"
                            :single-select="singleSelect"
                            :item-key="name" show-select
                            :headers="headers" :items="desserts"
                            sort-by="applied"
                            class="mr-2"
                        >
                        <template v-slot:top>
                            <v-toolbar flat color="white">
                                <v-toolbar-title>Applicants</v-toolbar-title>
                                <v-divider class="mx-4" inset vertical="">
                                </v-divider>
                                <v-spacer></v-spacer>
                                <v-btn color="grey lighten-1" dark class="mb-2 mr-2" v-on="on" text><v-icon left>fas fa-upload</v-icon>CSV Import</v-btn>
                                <v-btn color="success" dark class="mb-2" v-on="on" text><v-icon left>add</v-icon>ADD CANDIDATE</v-btn>
                            </v-toolbar>
                        </template>
                        <template v-slot:item.avatar="{ item }">
                            <v-avatar size="30px"><img :src="item.avatar"></v-avatar>
                        </template>
                        <template v-slot:item.rating="{ item }">
                            <v-rating v-model="item.rating" background-color="purple lighten-3" color="purple" small dense></v-rating>
                        </template>
                        <template v-slot:item.progress="{ item }">
                            <v-progress-linear color="light-blue" height="6" v-model="item.progress" stripped="">

                            </v-progress-linear>
                        </template>
                        <template v-slot:item.action="{ item }">
                            <v-icon small class="mr-2" @click="editItem(item)" color="green">edit</v-icon>
                            <v-icon small class="mr-2" @click="deleteItem(item)" color="red">delete</v-icon>
                        </template>
                        <template v-slot:no-data>
                            <v-btn color="primary" @click="initialize">Reset</v-btn>
                        </template>
                        </v-data-table>
                    </template>
                </v-container>
            </v-app>
        </v-flex>
    </v-layout>
</template>

<script>
export default {
    data: () => ({
        items: ['key1', 'key2', 'key3'],
        value: ['key1', 'key2', 'key3'],
        jobs: ['Designer', 'Dev'],
        job: ['Designer', 'Dev'],
        singleSelect: false,
        seleted: [],
        headers: [
            {text: 'PICTURE', align: 'right', sortable: false, value: 'avatar'},
            {text: 'APPLICANT', value: 'name'},
            {text: 'APPLIED ON', value: 'applied'},
            {text: 'PROGRESS', value: 'progress'},
            {text: 'RATING', value: 'rating'},
            {text: '', value: 'action', sortable: false },
        ]
    }),
    created() {
        this.initialize()
    },
    methods: {
        initialize() {
            this.desserts = [
                {avatar: '/img01.png', name:'Frozen Yogurt', applied: '02/04/2020', progress: 70, rating: 4 },
                {avatar: '/img02.png', name:'Black Coffee', applied: '04/01/2020', progress: 30, rating: 2 },
                {avatar: '/img03.png', name:'Rizen Fruit', applied: '03/20/2020', progress: 50, rating: 3 },
                {avatar: '/img02.png', name:'Lorem Ipsum', applied: '01/20/2020', progress: 76, rating: 5 },
                {avatar: '/img01.png', name:'Green Abacate', applied: '03/06/2020', progress: 52, rating: 1 },
                {avatar: '/img03.png', name:'Orange Fruit', applied: '04/04/2020', progress: 49, rating: 2 },
                {avatar: '/img02.png', name:'Keyboard Computer', applied: '02/04/2020', progress: 60, rating: 3 },
                {avatar: '/img03.png', name:'Rey Charles', applied: '03/18/2020', progress: 37, rating: 4 },
                {avatar: '/img01.png', name:'Dark Notebook', applied: '03/20/2020', progress: 41, rating: 5 }
            ]
        }
    }
}
</script>