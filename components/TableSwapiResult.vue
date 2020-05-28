<template>
  <b-container fluid>
    <!-- User Interface controls -->
    <b-row>
      <b-col sm="5" md="6" class="my-1">
      
          <b-form-select class="bg-secondary text-warning" variant="danger"
            v-model="perPage"
            id="perPageSelect"
            size="sm"
            :options="pageOptions"
          ></b-form-select>
        
      </b-col>
    </b-row>

    <!-- Main table element -->
    <b-table class="text-warning"
      show-empty
      small
      stacked="md"
      :items="items"
      :fields="fields"
      :current-page="currentPage"
      :per-page="perPage"
      :filter="filter"
      :filterIncludedFields="filterOn"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      :sort-direction="sortDirection"
      @filtered="onFiltered"
    >
      <template v-slot:cell(actions)="row">
        <b-button size="sm" @click="info(row.item, row.index, $event.target)" class="mr-1">
          Info modal
        </b-button>
        <b-button size="sm" @click="row.toggleDetails">
          {{ row.detailsShowing ? 'Hide' : 'Show' }} Details
        </b-button>
      </template>

      <template class="text-dark" v-slot:row-details="row">
        <b-card>
          <ul>
            <li class="text-dark" v-for="(value, key) in row.item" :key="key">{{ key }}: {{ value }}</li>
          </ul>
        </b-card>
      </template>
    </b-table>

    <!-- Info modal -->
    <b-modal class="bg-dark" :id="infoModal.id" :title="infoModal.title" ok-only @hide="resetInfoModal">
      <pre>{{ infoModal.content }}</pre>
    </b-modal>

    <b-col>
        <b-pagination 
          v-model="currentPage"
          :total-rows="totalRows"
          :per-page="perPage"
          align="fill"
          size="sm"
          class="my-0 bg-dark text-warning"
        ></b-pagination>
      </b-col>

  </b-container>
</template>

<script>
  export default {
    props:{
      items: {default: ()=> [
          { isActive: false, age: 27, name: { first: 'Essie', last: 'Dunlap' },example:  true },
          { isActive: true, age: 40, name: { first: 'Thor', last: 'Macdonald' },example: true },
          { isActive: true, age: 87,name: { first: 'Larsen', last: 'Shaw' },_cellVariants: { age: 'danger',
           isActive: 'warning'},example: false }
        ]},
        fields: {default: ()=> [
          { key: 'name', label: 'Person Full name', sortable: true, sortDirection: 'desc' },
          { key: 'age', label: 'Person age', sortable: true, class: 'text-center' },
          {key: 'example',label: 'example',sortable:true,class:'text-center'},
          {
            key: 'isActive',
            label: 'is Active',
           
            sortable: true,
            sortByFormatted: true,
            filterByFormatted: true
          },
          { key: 'actions', label: 'Actions' }
        ]}
    },
    data() {
      return {
        totalRows: 1,
        currentPage: 1,
        perPage: 5,
        pageOptions: [5, 10, 15],
        sortBy: '',
        sortDesc: false,
        sortDirection: 'asc',
        filter: null,
        filterOn: [],
        infoModal: {
          id: 'info-modal',
          title: '',
          content: ''
        }
      }
    },
    computed: {
      sortOptions() {
        // Create an options list from our fields
        return this.fields
          .filter(f => f.sortable)
          .map(f => {
            return { text: f.label, value: f.key }
          })
      }
    },
    mounted() {
      // Set the initial number of items
      this.totalRows = this.items.length
    },
    methods: {
      info(item, index, button) {
        this.infoModal.title = `Row index: ${index}`
        this.infoModal.content = JSON.stringify(item, null, 2)
        this.$root.$emit('bv::show::modal', this.infoModal.id, button)
      },
      resetInfoModal() {
        this.infoModal.title = ''
        this.infoModal.content = ''
      },
      onFiltered(filteredItems) {
        // Trigger pagination to update the number of buttons/pages due to filtering
        this.totalRows = filteredItems.length
        this.currentPage = 1
      }
    }
  }
</script>