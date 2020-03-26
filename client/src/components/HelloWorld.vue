<template>
    <b-container>
        <div>
            <b-table
                show-empty
                sticky-header="600px"
                small
                no-border-collapse
                responsive
                bordered
                :items="items"
                :fields="fields"
                :current-page="currentPage"
                :per-page="perPage"
                :filter="filterObj"
                :filter-function="filterTable"
                @filtered="onFiltered"
            >
                <template v-slot:head(name)="row">
                    {{ row.label }}
                </template>

                <template v-slot:cell(name)="row">
                    {{ row.value.first }} {{ row.value.last }}
                </template>

                <template v-slot:cell(experience)="row">
                    {{ row.value.join(', ') }}
                </template>
                <template v-slot:top-row>
                    <td>
                        <b-form-input
                            v-model="filterObj.name"
                            type="text"
                            placeholder="Type to Search"
                        ></b-form-input>
                    </td>
                    <td>
                        <b-form-input
                            v-model="filterObj.age"
                            type="number"
                            placeholder="Type to Search"
                        ></b-form-input>
                    </td>
                    <td>
                        <b-form-input
                            v-model="filterObj.birthday"
                            type="date"
                            placeholder="Type to Search"
                        ></b-form-input>
                    </td>
                    <td>
                        <b-form-select
                            v-model="filterObj.isActive"
                            :options="isActiveOptions"
                        ></b-form-select>
                    </td>
                    <td>
                        <b-form-select
                            v-model="filterObj.experience"
                            :options="isExpOptions"
                        ></b-form-select>
                    </td>
                </template>
            </b-table>
        </div>

        <b-row>
            <b-col sm="5" md="6" class="my-1">
                <b-form-group
                    label="Per page"
                    label-cols-sm="6"
                    label-cols-md="4"
                    label-cols-lg="3"
                    label-align-sm="right"
                    label-size="sm"
                    label-for="perPageSelect"
                    class="mb-0"
                >
                    <b-form-select
                        v-model="perPage"
                        id="perPageSelect"
                        size="sm"
                        :options="pageOptions"
                    ></b-form-select>
                </b-form-group>
            </b-col>

            <b-col sm="7" md="6" class="my-1">
                <b-pagination
                    v-model="currentPage"
                    :total-rows="totalRows"
                    :per-page="perPage"
                    align="fill"
                    size="sm"
                    class="my-0"
                ></b-pagination>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
export default {
    name: 'HelloWorld',
    props: {
        msg: String,
    },
    data() {
        return {
            items: [
                {
                    isActive: true,
                    age: 40,
                    name: {
                        first: 'Dickerson',
                        last:
                            'Macdonald фыво ыфво jdsakl dasjkld jasklj dlsa dsa dsad asd sad sadasdk shadk shakd sak dasd',
                    },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html'],
                },
                {
                    isActive: false,
                    age: 21,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 9,
                    name: { first: 'Mini', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 89,
                    name: { first: 'Geneva', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'Jami', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 27,
                    name: { first: 'Essie', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Thor', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 87,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 26,
                    name: { first: 'Mitzi', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 22,
                    name: { first: 'Genevieve', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'John', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 29,
                    name: { first: 'Dick', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Dickerson', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 21,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 9,
                    name: { first: 'Mini', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 89,
                    name: { first: 'Geneva', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'Jami', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 27,
                    name: { first: 'Essie', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Thor', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 87,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 26,
                    name: { first: 'Mitzi', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 22,
                    name: { first: 'Genevieve', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'John', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 29,
                    name: { first: 'Dick', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Dickerson', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 21,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 9,
                    name: { first: 'Mini', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 89,
                    name: { first: 'Geneva', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'Jami', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 27,
                    name: { first: 'Essie', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Thor', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 87,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 26,
                    name: { first: 'Mitzi', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 22,
                    name: { first: 'Genevieve', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'John', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 29,
                    name: { first: 'Dick', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Dickerson', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 21,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 9,
                    name: { first: 'Mini', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 89,
                    name: { first: 'Geneva', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'Jami', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 27,
                    name: { first: 'Essie', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 40,
                    name: { first: 'Thor', last: 'Macdonald' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 87,
                    name: { first: 'Larsen', last: 'Shaw' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 26,
                    name: { first: 'Mitzi', last: 'Navarro' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 22,
                    name: { first: 'Genevieve', last: 'Wilson' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: true,
                    age: 38,
                    name: { first: 'John', last: 'Carney' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
                {
                    isActive: false,
                    age: 29,
                    name: { first: 'Dick', last: 'Dunlap' },
                    date: '21.06.2000',
                    experience: ['Java', 'Css', 'Html', 'Node'],
                },
            ],
            isActiveOptions: [
                { value: null, text: '' },
                { value: true, text: 'Yes' },
                { value: false, text: 'No' },
            ],
            isExpOptions: [
                { value: null, text: '' },
                { value: 'Node', text: 'Node' },
                { value: 'Java', text: 'Java' },
                { value: 'Css', text: 'Css' },
                { value: 'Html', text: 'Html' },
            ],
            totalRows: 1,
            currentPage: 1,
            perPage: 10,
            filterObj: {
                name: null,
                age: null,
                birthday: null,
                isActive: null,
                experience: null,
            },
            pageOptions: [10, 20, 40, 100],
            filterOn: [],
            infoModal: {
                id: 'info-modal',
                title: '',
                content: '',
            },
        };
    },
    computed: {
        fields: function () {
            return [
                {
                    key: 'name',
                    stickyColumn: true,
                    label: 'Person Full name',
                    thClass: this.filterObj.name ? 'filtered' : '',
                },
                {
                    key: 'age',
                    label: 'Person age',
                    class: 'text-center',
                    thClass: this.filterObj.age ? 'filtered' : '',
                },
                {
                    key: 'date',
                    label: 'Birthday',
                    class: 'text-center',
                    thClass: this.filterObj.birthday ? 'filtered' : '',
                },
                {
                    key: 'isActive',
                    label: 'is Active',
                    formatter: (value) => {
                        return value ? 'Yes' : 'No';
                    },
                    filterByFormatted: true,
                    thClass: this.filterObj.isActive ? 'filtered' : '',
                },
                {
                    key: 'experience',
                    label: 'Experience',
                    class: 'text-center',
                    thClass: this.filterObj.experience ? 'filtered' : '',
                },
            ];
        },
    },
    mounted() {
        // Set the initial number of items
        this.totalRows = this.items.length;
        let thElm;
        let startOffset;
        [].forEach.call(document.querySelectorAll('table td'), function (td) {
            td.style.position = 'relative';

            let grip = document.createElement('div');
            grip.innerHTML = '&nbsp;';
            grip.style.top = '0';
            grip.style.right = '-10px';
            grip.style.bottom = '0';
            grip.style.width = '20px';
            grip.style.position = 'absolute';
            grip.style.cursor = 'col-resize';
            grip.addEventListener('mousedown', function (e) {
                thElm = td;
                startOffset = td.offsetWidth - e.pageX;
            });

            td.appendChild(grip);
        });

        document.addEventListener('mousemove', function (e) {
            if (thElm) {
                thElm.style.width = startOffset + e.pageX + 'px';
            }
        });

        document.addEventListener('mouseup', function () {
            thElm = undefined;
            startOffset = undefined;
        });
    },
    methods: {
        onFiltered(filteredItems) {
            // Trigger pagination to update the number of buttons/pages due to filtering
            this.totalRows = filteredItems.length;
            this.currentPage = 1;
        },
        filterTable(row, filter) {
            if (
                filter.name &&
                (row.name.first + ' ' + row.name.last).indexOf(filter.name) ===
                    -1
            ) {
                return false;
            }

            if (filter.age && row.age.toString().indexOf(filter.age) === -1) {
                return false;
            }

            if (
                filter.experience &&
                row.experience.join(', ').indexOf(filter.experience) === -1
            ) {
                return false;
            }

            if (filter.birthday) {
                const [yy, mm, dd] = filter.birthday.split('-');
                if (`${dd}.${mm}.${yy}`.indexOf(row.date) === -1) {
                    return false;
                }
            }

            if (filter.isActive !== null && filter.isActive !== row.isActive) {
                return false;
            }
            return true;
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}
</style>
