<template>
  <div class="panel panel-success" :id="idTable">
    <div class="panel-heading">
      <slot name="table-top"></slot>
    </div>
    <div class="panel-body">
      <div class="table-responsive">
        <table class="table table-striped">
          <thead>
            <tr>
              <th v-for="(header, index) in headers" :key="index" :width="header.width" style="text-align: center">{{ header.title }}</th>
            </tr>
          </thead>
          <tbody v-if="items.length">
            <tr v-for="(item, index) in items" :key="index">
              <td v-for="(header, index) in headers" :key="index" :style="{textAlign: header.align}">
                <slot :name="header.value" :item="item">{{ item[header.value] || '' }}</slot>
              </td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td :colspan="headers.length" style="text-align: center">
                Sem Resultados
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'TableComponent',

  props: {
    headers: {
        type: Array,
        required: true,
    },
    items: {
        type: Array,
        required: true,
    },
  },

  data: () => ({
    idTable: new Date().getTime(),
  }),
};
</script>
