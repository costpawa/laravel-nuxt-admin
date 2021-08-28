<template>
  <div class="m-1 table-container">
    <md-table v-model="datas" md-sort="id" md-sort-order="asc" md-card md-fixed-header @md-selected="onSelect">
      <md-table-toolbar slot="md-table-alternate-header" slot-scope="{ count }">
        <div class="md-toolbar-section-start">{{ getAlternateLabel(count) }}</div>
        <div class="md-toolbar-section-end">
          <md-button class="md-icon-button">
            <md-icon>delete</md-icon>
          </md-button>
        </div>
      </md-table-toolbar>
      <md-table-toolbar>
        <h1 class="md-title">All {{ pageTitle }}</h1>
      </md-table-toolbar>

      <md-table-row slot="md-table-row" slot-scope="{ item }" md-selectable="multiple" md-auto-select>
        <md-table-cell md-label="ID" md-sort-by="id">{{ item.id }}</md-table-cell>
        <md-table-cell md-label="Company" md-sort-by="company">{{ item.company }}</md-table-cell>
        <md-table-cell md-label="Vat" md-sort-by="vat">{{ item.vat }}</md-table-cell>
        <md-table-cell md-label="Address" md-sort-by="address">{{ item.address }}</md-table-cell>
        <md-table-cell md-label="Operations">
          <NuxtLink :to="`/${page}/${item.id}`">
            <md-button class="md-icon-button md-dense md-primary">
              <md-icon style="color: #858598;" title="Show">visibility</md-icon>
            </md-button>
          </NuxtLink>
          <NuxtLink :to="`/${page}/${item.id}/edit`">
            <md-button class="md-icon-button md-dense md-primary">
              <md-icon title="Edit">edit</md-icon>
            </md-button>
          </NuxtLink>
          <NuxtLink :to="`/${page}/${item.id}/delete`">
            <md-button class="md-icon-button md-dense md-accent">
              <md-icon title="Delete">delete</md-icon>
            </md-button>
          </NuxtLink>
        </md-table-cell>
      </md-table-row>

    </md-table>
    <!-- <p>Selected:</p>
    {{ selected }} -->
  </div>
</template>

<script>
  export default {
    name: 'TableCard',
    props: ['page','pageTitle'],
    data: () => ({
      selected: [],
      datas: [
        {
          id: 1,
          company: "Shawna Dubbin",
          vat: "12346",
          address: "Account Coordinator"
        },
        {
          id: 2,
          company: "Odette Demageard",
          vat: "odemageard1@spotify.com",
          address: "Account Coordinator"
        },
        {
          id: 3,
          company: "Vera Taleworth",
          vat: "vtaleworth2@google.ca",
          address: "Community Outreach Specialist"
        },
        {
          id: 4,
          company: "Lonnie Izkovitz",
          vat: "lizkovitz3@youtu.be",
          address: "Operator"
        },
        {
          id: 5,
          company: "Thatcher Stave",
          vat: "tstave4@reference.com",
          address: "Software Test Engineer III"
        }
      ]
    }),
    methods: {
      onSelect (items) {
        this.selected = items
      },
      getAlternateLabel (count) {
        let plural = ''

        if (count > 1) {
          plural = 's'
        }

        return `${count} data${plural} selected`
      }
    }
  }
</script>
