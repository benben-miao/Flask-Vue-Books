<template>
  <div style="margin: 0px; padding: 100px;">
    <div style="width: 100%;">
      <h1>Book Manager System</h1>
      <el-button type="primary" size="small" @click="addDialogVisible = true">
        New Book
      </el-button>
    </div>
    <el-table :data="books" style="margin: 20px auto;">
      <el-table-column label="Number" prop="book_number" />
      <el-table-column label="Name" prop="book_name" />
      <el-table-column label="Type" prop="book_type" />
      <el-table-column label="Prize" prop="book_prize" />
      <el-table-column label="Author" prop="author" />
      <el-table-column label="Publisher" prop="book_publisher" />
      <el-table-column align="right" label="Options" width="200px">
        <template #default="scope">
          <el-button size="small" @click="handleEdit(scope.$index, scope.row)">
            Edit
          </el-button>
          <el-button size="small" type="danger" @click="handleDelete(scope.$index, scope.row)">
            Delete
          </el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-dialog title="New Book" v-model="addDialogVisible" width="50%" :before-close="handleClose" style="padding: 20px;">
      <el-form ref="ruleFormRef" :model="book_form" status-icon label-width="100px" class="ruleForm">
        <el-form-item label="Number" prop="book_number">
          <el-input v-model="book_form.book_number" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Name" prop="book_name">
          <el-input v-model="book_form.book_name" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Type" prop="book_type">
          <el-input v-model="book_form.book_type" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Prize" prop="book_prize">
          <el-input v-model="book_form.book_prize" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Author" prop="author">
          <el-input v-model="book_form.author" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Publisher" prop="book_publisher">
          <el-input v-model="book_form.book_publisher" autocomplete="off"/>
        </el-form-item>
        
        <el-form-item>
          <el-button type="primary" @click="submitForm(ruleFormRef)">
            Submit
          </el-button>
          <el-button @click="resetForm(ruleFormRef)">
            Reset
          </el-button>
        </el-form-item>
      </el-form>
    </el-dialog>

    <el-dialog title="New Book" v-model="editDialogVisible" width="50%" :before-close="handleClose" style="padding: 20px;">
      <el-form ref="editFormRef" :model="book_form" status-icon label-width="100px" class="ruleForm">
        <el-form-item label="Number" prop="book_number">
          <el-input v-model="book_form.book_number" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Name" prop="book_name">
          <el-input v-model="book_form.book_name" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Type" prop="book_type">
          <el-input v-model="book_form.book_type" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Prize" prop="book_prize">
          <el-input v-model="book_form.book_prize" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Author" prop="author">
          <el-input v-model="book_form.author" autocomplete="off"/>
        </el-form-item>
        <el-form-item label="Publisher" prop="book_publisher">
          <el-input v-model="book_form.book_publisher" autocomplete="off"/>
        </el-form-item>
        
        <el-form-item>
          <el-button type="primary" @click="submitEditForm(editFormRef)">
            Submit
          </el-button>
          <el-button @click="resetForm(editFormRef)">
            Reset
          </el-button>
        </el-form-item>
      </el-form>
    </el-dialog>
  </div>
</template>

<script setup>
import axios from 'axios'
import { reactive, ref, onMounted } from 'vue'
import { ElMessageBox } from 'element-plus'

const books = reactive([])

const getBooks = () => {
  axios.get("http://127.0.0.1:5000/books/",)
    .then(res => {
      books.splice(0, books.length)
      books.push(...res.data.results)
      // console.log(res.data)
    } )
}

onMounted(() => {
  getBooks()
})

const handleDelete = (index, scope) => {
  axios.delete(`http://127.0.0.1:5000/books/${scope.id}`)
  .then(() => {
    getBooks()
  })
}

const addDialogVisible = ref(false)
const ruleFormRef = ref()
const book_form = reactive({
  book_number: "",
  book_name: "",
  book_type: "",
  book_prize: "",
  author: "",
  book_publisher: "",
  id: ""
})

const submitForm = (formEl) => {
  axios.post("http://127.0.0.1:5000/books", book_form)
  .then(() => {
    addDialogVisible = false
    formEl.resetFields()
    getBooks()
  })
}

const resetForm = (formEl) => {
  formEl.resetFields()
}

const handleClose = (done) => {
  ElMessageBox.confirm("Confirm to close the window?")
  .then(() => {
    done();
  })
  .catch(() => {

  })
}

const editFormRef = ref()
const editDialogVisible = ref(false)
const handleEdit = (index, scope) => {
  for (let key in scope) {
    book_form[key] = scope[key]
  }
  editDialogVisible.value = true
}

const submitEditForm = (formEl) => {
  axios.put(`http://127.0.0.1:5000/books/${book_form.id}`, book_form)
  .then((res) => {
    formEl.resetFields()
    editDialogVisible.value = false
    getBooks()
  })
}
</script>

<style scoped>

</style>
