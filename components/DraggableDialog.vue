<template>
  <div>
    <el-dialog v-model="dialogVisible" title="Tanlang" width="500" draggable>
      <el-tabs v-model="form.type" type="border-card">

        <!-- tab 1 -->
        <el-tab-pane name="word" label="So'z">
          <el-form :model="form" label-width="auto" style="max-width: 600px">
            <el-form-item label="So'z (simvol)">
              <el-input @keyup.enter="save" v-model="form.text"></el-input>
            </el-form-item>
            <el-form-item label="Sarlavha">
              <el-input @keyup.enter="save" v-model="form.title"></el-input>
            </el-form-item>
            <el-form-item label="Katak rangi">
              <el-color-picker v-model="form.backgroundColor" show-alpha :predefine="predefineColors" />
            </el-form-item>
            <el-form-item label="So'z rangi">
              <el-color-picker v-model="form.color" show-alpha :predefine="predefineColors" />
            </el-form-item>
          </el-form>
        </el-tab-pane>

        <!-- tab 2 -->
        <el-tab-pane name="photo" label="Surat">
          <el-upload
            class="upload-demo"
            drag
            action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
            multiple
          >
            <el-icon class="el-icon--upload"><upload-filled /></el-icon>
            <div class="el-upload__text">
              Faylni shu yerga tashlang yoki <em>yuklash uchun bosing</em>
            </div>
            <template #tip>
              <div class="el-upload__tip">
                Fayl hajmi 500 kb dan kam bo'lishi kerak (jpg/png)
              </div>
            </template>
          </el-upload>
        </el-tab-pane>

      </el-tabs>
      <template #footer>
        <div class="dialog-footer">
          <el-button @click="dialogVisible = false">Bekor qilish</el-button>
          <el-button type="primary" @click="save">
            Saqlash
          </el-button>
        </div>
      </template>
    </el-dialog>
  </div>
</template>

<script lang="ts" setup>
import { UploadFilled } from '@element-plus/icons-vue';
const emit = defineEmits(['opcao-emit'])

const dialogVisible = ref(false);
const formKeys = {
  type: 'word',
  title: '',
  photo: '',
  backgroundColor: '',
  color: '',
  text: ''
};

const form = ref(JSON.parse(JSON.stringify(formKeys)))

const color = ref('rgba(255, 69, 0, 0.68)')
const predefineColors = ref([
  '#ff4500',
  '#ff8c00',
  '#ffd700',
  '#90ee90',
  '#00ced1',
  '#1e90ff',
  '#c71585',
  'rgba(255, 69, 0, 0.68)',
  'rgb(255, 120, 0)',
  'hsv(51, 100, 98)',
  'hsva(120, 40, 94, 0.5)',
  'hsl(181, 100%, 37%)',
  'hsla(209, 100%, 56%, 0.73)',
  '#c7158577',
])

// methods
const open = () => {
  dialogVisible.value = true;
};
const save = () => {
  emit('form', JSON.parse(JSON.stringify(form)));
  dialogVisible.value = false;
  form.value = JSON.parse(JSON.stringify(formKeys));
};

defineExpose({
  open
});

function defineExpose(arg0: { open: () => void; }) {
  throw new Error("Function not implemented.");
}
</script>