<template>
  <a-modal
    title="预览"
    :visible="visible"
    @ok="handleGetData"
    @cancel="handleCancel"
    okText="获取数据"
    cancelText="关闭"
    style="top:20px;"
    :destroyOnClose="true"
    :width="`${previewWidth}px`"
  >
    <k-build-form
      :jsonData="jsonData"
      @submit="handleSubmit"
      ref="kBuildForm"
    />
    <jsonModel ref="jsonModel" />
  </a-modal>
</template>
<script>
import jsonModel from "./jsonModal";
export default {
  name: "previewModal",
  data() {
    return {
      visible: false,
      previewWidth: 850,
      jsonData: {}
    };
  },
  components: {
    jsonModel
  },
  methods: {
    handleSubmit(p) {
      p.then(res => {
        console.log(res, "获取数据成功");
        this.$refs.jsonModel.jsonData = res;
        this.$refs.jsonModel.visible = true;
      }).catch(err => {
        console.log(err, "获取数据失败");
      });
    },
    handleGetData() {
      this.$refs.kBuildForm
        .getData()
        .then(res => {
          console.log(res, "获取数据成功");
          this.$refs.jsonModel.jsonData = res;
          this.$refs.jsonModel.visible = true;
        })
        .catch(err => {
          console.log(err, "获取数据失败");
        });
    },
    handleCancel() {
      this.visible = false;
    }
  }
};
</script>
