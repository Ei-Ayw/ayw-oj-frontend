<template>
  <div id="manageQuestionView">
    <a-table
      :ref="tableRef"
      :columns="columns"
      :data="dataList"
      :pagination="{
        showTotal: true,
        pageSize: searchParams.pageSize,
        current: searchParams.current,
        total,
      }"
      @page-change="onPageChange"
    >
      <template #tags="{ record }">
        <a-space wrap>
          <!-- 如果 record.tags 是字符串，先解析为数组 -->
          <template v-if="typeof record.tags === 'string'">
            <a-tag
              v-for="(tag, index) in JSON.parse(record.tags)"
              :key="index"
              color="green"
            >
              {{ tag }}
            </a-tag>
          </template>
          <!-- 如果 record.tags 已经是数组，直接渲染 -->
          <template v-else-if="Array.isArray(record.tags)">
            <a-tag
              v-for="(tag, index) in record.tags"
              :key="index"
              color="green"
            >
              {{ tag }}
            </a-tag>
          </template>
        </a-space>
      </template>
      <template #[judgeConfig]="{ text }">
        <div class="judge-config">
          <template>
            <div
              v-for="(value, key) in JSON.parse(text)"
              :key="key"
              class="config-item"
            >
              <span class="label">{{ key }}：</span>
              <span class="value">{{ value }}</span>
            </div>
          </template>
        </div>
      </template>
      <template #createTime="{ record }">
        {{ moment(record.createTime).format("YYYY-MM-DD") }}
      </template>
      <template #optional="{ record }">
        <a-space>
          <a-button type="primary" @click="doUpdate(record)"> 修改</a-button>
          <a-button status="danger" @click="doDelete(record)">删除</a-button>
        </a-space>
      </template>
    </a-table>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, watchEffect } from "vue";
import {
  Page_Question_,
  Question,
  QuestionControllerService,
} from "../../../generated";
import message from "@arco-design/web-vue/es/message";
import * as querystring from "querystring";
import { useRouter } from "vue-router";
import moment from "moment/moment";

const tableRef = ref();

const dataList = ref([]);
const total = ref(0);
const searchParams = ref({
  pageSize: 10,
  current: 1,
});

const loadData = async () => {
  const res = await QuestionControllerService.listQuestionByPageUsingPost(
    searchParams.value
  );
  if (res.code === 0) {
    dataList.value = res.data.records;
    console.log("data" + dataList.value);
    total.value = res.data.total;
  } else {
    message.error("加载失败，" + res.message);
  }
};

/**
 * 监听 searchParams 变量，改变时触发页面的重新加载
 */
watchEffect(() => {
  loadData();
});

/**
 * 页面加载时，请求数据
 */
onMounted(() => {
  loadData();
});

// {id: "1", title: "A+ D", content: "新的题目内容", tags: "["二叉树"]", answer: "新的答案", submitNum: 0,…}

const columns = [
  {
    title: "id",
    dataIndex: "id",
  },
  {
    title: "标题",
    dataIndex: "title",
    width: 120, // 设置内容列的宽度为200px
    ellipsis: true, // 超出部分显示省略号
    tooltip: true, // 鼠标悬停时显示完整内容
  },
  {
    title: "内容",
    dataIndex: "content",
    width: 200, // 设置内容列的宽度为200px
    ellipsis: true, // 超出部分显示省略号
    tooltip: true, // 鼠标悬停时显示完整内容
  },
  {
    title: "标签",
    slotName: "tags",
  },
  // {
  //   title: "答案",
  //   dataIndex: "answer",
  // },
  {
    title: "提交数",
    dataIndex: "submitNum",
    width: 100, // 设置内容列的宽度为200px
  },
  {
    title: "通过数",
    dataIndex: "acceptedNum",
    width: 100, // 设置内容列的宽度为200px
  },
  // {
  //   title: "判题配置",
  //   slotName: "judgeConfig",
  // },
  // {
  //   title: "判题用例",
  //   dataIndex: "judgeCase",
  // },
  // {
  //   title: "用户id",
  //   dataIndex: "userId",
  // },
  {
    title: "创建时间",
    slotName: "createTime",
  },
  {
    title: "操作",
    slotName: "optional",
  },
];

const onPageChange = (page: number) => {
  searchParams.value = {
    ...searchParams.value,
    current: page,
  };
};

const doDelete = async (question: Question) => {
  const res = await QuestionControllerService.deleteQuestionUsingPost({
    id: question.id,
  });
  if (res.code === 0) {
    message.success("删除成功");
    loadData();
  } else {
    message.error("删除失败");
  }
};

const router = useRouter();

const doUpdate = (question: Question) => {
  router.push({
    path: "/update/question",
    query: {
      id: question.id,
    },
  });
};
</script>

<style scoped>
#manageQuestionView {
  max-width: 1280px;
  margin: 0 auto;
}
</style>
