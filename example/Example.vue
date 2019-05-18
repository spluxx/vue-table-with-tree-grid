<template lang="html">
  <div id="example">
    <zk-table
      ref="table"
      sum-text="sum"
      index-text="#"
      :data="data"
      :columns="columns"
      :stripe="props.stripe"
      :border="props.border"
      :show-header="props.showHeader"
      :show-summary="props.showSummary"
      :show-row-hover="props.showRowHover"
      :show-index="props.showIndex"
      :tree-type="props.treeType"
      :is-fold="props.isFold"
      :expand-type="props.expandType"
      :selection-type="props.selectionType">
      <template slot="$expand" scope="scope">
        {{ `My name is ${scope.row.name},
           this rowIndex is ${scope.rowIndex}.`
         }}
      </template>
      <template slot="likes" scope="scope">
        <input type="button" v-on:change="fileChanged($event, scope.row.files)" accept="image/*" multiple/>
        {{ scope.row.likes.join(',') }}
      </template>
    </zk-table>

    <button @click="deleteAll"> Delete All </button>
  </div>
</template>

<script>
  import ZkSwitch from './Switch/Switch';

  export default {
    name: 'example',
    components: {
      ZkSwitch,
    },
    data() {
      return {
        props: {
          stripe: false,
          border: false,
          showHeader: true,
          showSummary: false,
          showRowHover: true,
          showIndex: false,
          treeType: true,
          isFold: true,
          expandType: false,
          selectionType: false,
        },
        data: [
          {
            name: 'Jack',
            sex: 'male',
            likes: ['football', 'basketball'],
            score: 10,
            _children: [
              {
                name: 'Ashley',
                sex: 'female',
                likes: ['football', 'basketball'],
                score: 20,
                _children: [
                  {
                    name: 'Taki',
                    sex: 'male',
                    likes: ['football', 'basketball'],
                    score: 10,
                    _children: [],
                  },
                ],
              },
            ],
          },
          {
            name: 'Jack',
            sex: 'male',
            likes: ['football', 'basketball'],
            score: 10,
            _children: [
              {
                name: 'Ashley',
                sex: 'female',
                likes: ['football', 'basketball'],
                score: 20,
                _children: [
                  {
                    name: 'Taki',
                    sex: 'male',
                    likes: ['football', 'basketball'],
                    score: 10,
                    _children: [],
                  },
                ],
              },
            ],
          },
        ],
        columns: [
          {
            label: 'name',
            prop: 'name',
            width: '400px',
          },
          {
            label: 'sex',
            prop: 'sex',
            minWidth: '50px',
          },
          {
            label: 'score',
            prop: 'score',
          },
          {
            label: 'likes',
            prop: 'likes',
            minWidth: '200px',
            type: 'template',
            template: 'likes',
          },
        ],
      };
    },
    computed: {
      propList() {
        return Object.keys(this.props).map(item => ({
          name: item,
        }));
      },
    },
    methods: {
      fileChanged(evt, files) {
        console.log(files);
      },
      deleteAll() {
        this.data.splice(0, 1);
        console.log(this.data);
      },
    },
  };
</script>

<style scoped lang="less">
  * {
    margin: 0;
    padding: 0;
  }

  .switch-list {
    margin: 20px 0;
    list-style: none;
    overflow: hidden;
  }

  .switch-item {
    margin: 20px;
    float: left;
  }
</style>
