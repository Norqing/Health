<template>
  <q-page padding>
    <div class="q-my-md">
      一般健康评量表（GUQ-12）
    </div>

    <div class="text-h5 q-my-md">
      本次测评共有12道题，请阅读后认真选出最适合您的答案，以下问题是针对从2-3周前到现在的状况，请选择最合适的一项。
    </div>

    <q-separator />
    <div class="q-my-md" v-for="(question, index) in questions" :key="index">
      <div>{{ index + 1 }}. {{ question.text }}</div>
      <q-option-group
        v-model="question.selected"
        :options="question.options"
        inline
        type="radio"
      />

    </div>
    <q-btn color="primary" @click="submitResults" label="提交问卷结果" />
    <div v-if="scoreMessage" class="q-mt-lg text-subtitle1">
      经过测评，您的一般心理测评分数为: <span class="text-red">{{ totalScore }}</span><br>
      测评结果为: <span class="text-red">{{ scoreMessage }}</span>
    </div>

  </q-page>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const questions = ref([
      // 问题数组初始化，包含问题文本和选项
      {
        text: '1.能集中精力于你做的任何事情吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      },
      {
        text: '2.由于焦虑而失眠？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      },
      {
        text: '3.感到对事物发挥作用了吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '4.感到对事物能做决定吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '5.一直感到精神紧张',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '6.感到不能克服困难',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '7.能喜欢日常的活动吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '8.能不回避矛盾吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '9.感到不高兴和抑郁？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '10.对自己失去信心了吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '11.认为自己是一个没有价值的人？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }, {
        text: '12.总的来看，感到适度的愉快吗？',
        options: [
          { label: '经常', value: 1 },
          { label: '有时', value: 2 },
          { label: '很少', value: 3 },
          { label: '从不', value: 4 }
        ],
        selected: null
      }
    ])

    const totalScore = ref(0)
    const scoreMessage = ref('')

    function submitResults () {
      totalScore.value = questions.value.reduce((sum, question) => sum + (question.selected || 0), 0)
      scoreMessage.value = totalScore.value > 27
        ? '根据国际一般健康问卷的评分机制，您的心理健康状况不佳。'
        : '根据国际一般健康问卷的评分机制，您的心理健康良好。'
    }

    return { questions, submitResults, totalScore, scoreMessage }
  }
}
</script>
  <style scoped>
      .text-green {
        color: green;
      }
      .text-red {
        color: red;
      }
      </style>
