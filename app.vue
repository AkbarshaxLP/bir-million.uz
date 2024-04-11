<template>
  <div class="container mx-auto pt-6">
    <!-- <pre>pixelsList: {{pixelsList}}</pre> -->
    <PixelsWrapper :length="sqLength">
      <template v-if="rendered" >
        <template v-for="(i, index_1) in sqLength">
          <TenPixels
            v-for="(j, index_2) in sqLength"
            :key="`${i}_${j}`"
            :value="pixelsList[`${index_1}_${index_2}`]"
            @click="draggableDialogOpen(`${index_1}_${index_2}`)"
          />
        </template>
      </template>
    </PixelsWrapper>
    <DraggableDialog @form="formChanged" ref="draggableDialog" />
  </div>
</template>


<script setup>
import { onMounted, ref } from 'vue';

const set_uuid = () => {
  if (process.client) {
    if (!localStorage.m_uuid) {
      const moonLanding = new Date();
      localStorage.m_uuid = moonLanding.getTime();
    };
    m_uuid.value = localStorage.m_uuid;
  }
};
const fill_list = () => {
  for (let i = 0; i < sqLength.value; i++) {
    for (let j = 0; j < sqLength.value; j++) {
      pixelsList.value[`${i}_${j}`] = null;
    }
  };
};
const fetchList = async () => {
  const data  = await $fetch(`http://localhost:3001/list/`);
  iterateList(data);
};

const m_uuid = ref(null)
const rendered = ref(true);
const selectedKey = ref('');
const pixelsList = ref({});
const sqLength = ref(40);
const draggableDialog = ref(null);

set_uuid();
fill_list();
fetchList();

const iterateList = (data) => {
  data.forEach(element => {
    pixelsList.value[element.key] = element;
  });
  forceRender();
};
const formChanged = (val) => {
  pixelsList.value[selectedKey.value] = val._value;
  saveToDB(val._value);
  forceRender();
};
const draggableDialogOpen = (val) => {
  selectedKey.value = val;
  draggableDialog.value.open();
};
const forceRender = async () => {
  rendered.value = false;
  await nextTick();
  rendered.value = true;
};

const saveToDB = async (val) => {
  const body = {
    key: selectedKey.value,
    m_uuid: m_uuid._value,
    ...val
  };

  await $fetch(`http://localhost:3001/list/`, {
    method: 'POST',
    body: body
  });
  fetchList();
}
</script>