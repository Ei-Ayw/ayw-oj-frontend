<template>
  <div id="questionSubmitView">
    <a-form :model="searchParams" layout="inline">
      <a-form-item field="questionId" label="题号" style="min-width: 240px">
        <a-input v-model="searchParams.questionId" placeholder="请输入" />
      </a-form-item>
      <a-form-item field="language" label="编程语言" style="min-width: 240px">
        <a-select
          v-model="searchParams.language"
          :style="{ width: '320px' }"
          placeholder="选择编程语言"
        >
          <a-option>java</a-option>
          <a-option>cpp</a-option>
          <a-option>go</a-option>
          <a-option>html</a-option>
        </a-select>
      </a-form-item>
      <a-form-item>
        <a-button type="primary" @click="doSubmit">搜索</a-button>
      </a-form-item>
    </a-form>
    <a-divider size="0" />
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
      <template #judgeInfo="{ record }">
        <div class="tag-container">
          <div
            v-for="(value, key, index) in record.judgeInfo"
            :key="key"
            class="tag"
            :class="getTagClass(value)"
          >
            <span class="tag-value">
              {{
                value
                  ? value + getUnit(key)
                  : index === 0
                  ? "判题中" + getUnit(key)
                  : index === 1
                  ? "0" + getUnit(key)
                  : index === 2
                  ? "0" + getUnit(key)
                  : ""
              }}
            </span>
          </div>
        </div>
      </template>
      <template #createTime="{ record }">
        {{ moment(record.createTime).format("YYYY-MM-DD") }}
      </template>
    </a-table>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, watchEffect } from "vue";
import {
  Question,
  QuestionControllerService,
  QuestionSubmitQueryRequest,
} from "../../../generated";
import message from "@arco-design/web-vue/es/message";
import { useRouter } from "vue-router";
import moment from "moment";

const tableRef = ref();

const dataList = ref([]);
const total = ref(0);
const searchParams = ref<QuestionSubmitQueryRequest>({
  questionId: undefined,
  language: undefined,
  pageSize: 10,
  current: 1,
});

const getUnit = function (key: any) {
  switch (key) {
    case "memory":
      return " MB"; // 内存单位为MB
    case "time":
      return " ms"; // 时间单位为毫秒
    default:
      return ""; // 其他键不添加单位
  }
};

const getTagClass = function (value: any) {
  if (value === "Accepted") {
    return "tag-accepted";
  } else if (!isNaN(value)) {
    return "tag-tag-normal";
  } else {
    return "tag-rejected";
  }
};

const loadData = async () => {
  const res = await QuestionControllerService.listQuestionSubmitByPageUsingPost(
    {
      ...searchParams.value,
      sortField: "createTime",
      sortOrder: "descend",
    }
  );
  if (res.code === 0) {
    dataList.value = res.data.records;
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

const columns = [
  {
    title: "提交号",
    dataIndex: "id",
  },
  {
    title: "编程语言",
    dataIndex: "language",
  },
  {
    title: "判题信息",
    slotName: "judgeInfo",
  },
  {
    title: "判题状态",
    dataIndex: "status",
  },
  {
    title: "题目 id",
    dataIndex: "questionId",
  },
  {
    title: "提交者 id",
    dataIndex: "userId",
  },
  {
    title: "创建时间",
    slotName: "createTime",
  },
];

const onPageChange = (page: number) => {
  searchParams.value = {
    ...searchParams.value,
    current: page,
  };
};

const router = useRouter();

/**
 * 跳转到做题页面
 * @param question
 */
const toQuestionPage = (question: Question) => {
  router.push({
    path: `/view/question/${question.id}`,
  });
};

/**
 * 确认搜索，重新加载数据
 */
const doSubmit = () => {
  // 这里需要重置搜索页号
  searchParams.value = {
    ...searchParams.value,
    current: 1,
  };
};
</script>

<style scoped>
#questionSubmitView {
  max-width: 1280px;
  margin: 0 auto;
}
.tag-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  padding: 10px;
  border-radius: 10px;
}

.tag {
  background: linear-gradient(to right, #a1c4fd, #c2e9fb); /* 渐变背景 */
  border: none;
  border-radius: 20px; /* 圆角 */
  padding: 8px 16px;
  font-family: "Arial", sans-serif;
  font-size: 14px;
  color: #333;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* 阴影 */
  display: flex;
  align-items: center;
}

.tag-value {
  font-style: normal; /* 正常字体 */
}

.tag-accepted {
  background: linear-gradient(to right, #aaffb1, #c8f7c4); /* 绿色渐变 */
}

.tag-rejected {
  background: linear-gradient(to right, #ff9999, #ffcccc); /* 红色渐变 */
}

.tag-normal {
  background: linear-gradient(to right, #e6f7ff, #c2e9fb); /* 正常颜色渐变 */
}
</style>
