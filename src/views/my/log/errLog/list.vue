<!-- 列表 -->
<template>
  <div class="list">
    <el-table :data="list">
      <el-table-column width="80" label="ID" prop="id"></el-table-column>
      <el-table-column prop="msg" label="错误信息"></el-table-column>
      <el-table-column width="140" label="错误方法">
        <template slot-scope="item">
          <span>{{item.row.module}}/{{item.row.controller}}/{{item.row.action}}</span>
        </template>
      </el-table-column>
      <el-table-column width="180" label="时间">
        <template slot-scope="item">
          <span>{{item.row.create_time}}</span>
        </template>
      </el-table-column>
      <el-table-column fixed="right" label="操作" align="center" width="180">
        <template slot-scope="item">
          <span v-on:click="del(item.row.id)" class="active pointer marginr20">删除</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script type='text/ecmascript-6'>
import imgs from "components/imgs";
export default {
  name: "list",
  props: {
    list: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  components: {
    imgs
  },
  methods: {
    async del(id) {
      let param = {
        data: { id: id },
        url: "/Api/Admin/ErrorLog/del",
        type: "POST"
      };
      let res = await this.request(param, "POST");
      this.utils.success("删除成功!");
      await this.$parent.getList();
    }
  }
};
</script>
